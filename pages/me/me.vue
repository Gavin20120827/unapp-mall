<template>
	<form class="form-block page">
		<view class="form-title">请输入您的会员账号</view>
		<view class="form-input">
			<input type="text" name="username" value="" class="username form-class" placeholder="请输入账号"/>
			<input type="text" name="password" placeholder="请输入密码" class="password form-class"/>
		</view>
		<view class="form-button-block">
			<view class="form-desc">请正确填写账号信息，有问题联系客服</view>
			<button type="primary" class="form-login">登录</button>
			<button type="primary" class="form-reg" @click="reg">注册新用户</button>
			<button type="warn" class="form-logout" open-type="getUserInfo" @getuserinfo="getUserInfo">微信登录</button>
<!-- 			<button type=" default" open-type="getPhoneNumber" @getphonenumber="getphonenumber">获取手机号</button>
 -->		</view>
		
		
		<!-- 直接获取到用户的昵称和头像等，未登录也可以获取 -->
	<!-- 	<open-data type="userNickName"></open-data>
		<view  style="width: 50upx;"><open-data type="userAvatarUrl"></open-data></view>
		<open-data type="userGender"></open-data> -->
	</form>
	
	
	

</template>

<script>
	import common from "../../common/common.js"
	
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			//跳转注册页面
			reg:function(){				
				uni.navigateTo({
					url: '/pages/me/reg/reg'
				});
			},
			
			//获取手机号流程
			getphonenumber:function(e){
				
				//获取到detail中的数据
				// console.log(e.detail.iv);
				var ivObj = e.detail.iv
				var phoneObj = e.detail.encryptedData
				var code = ''
				
				//获取code
				uni.login({
					success(res) {
						console.log(res.code)
						
						uni.request({
							url: 'https://api.weixin.qq.com/sns/jscode2session',
							method: 'GET',
							data: {
								 appid:'wxee7e0d5161c61923',
								 secret:'0e32dd95e20b576d6de4e5df32778519',
							     code: res.code,
							     encryptedData: phoneObj,
							     iv: ivObj
							},
							success: res => {
								console.log(res)
							}
						});
						
						if (e.detail.errMsg == 'getPhoneNumber:user deny') { //用户点击拒绝
						            wx.navigateTo({
						              url: '',
						            })
						          } else { //允许授权执行跳转
						            wx.navigateTo({
						              url: '',
						            })
						          }
					}
				})
				
			},
			
			//微信登录流程。两步，第一是获取通用信息(在button中定义getuserinfo，然后执行getuserinof函数就好了)；第二是获取openid
			getUserInfo:function(e){
				var serverUrl = common.serverUrl
				var nickName = ''
				var avatarUrl = ''
				var openid = ''
				
				//获取通用信息并且赋值
				uni.getUserInfo({
					success() {
						// console.log(e.detail.userInfo)
						nickName =  e.detail.userInfo.nickName
						avatarUrl = e.detail.userInfo.avatarUrl
					}
				})
				
				//获取openid并且写入数据库，缓存的流程
				//获取到code
				uni.login({
					success: res => {
						// console.log(res.code)
						
						//利用code，进一步获得openid
						uni.request({
							url: 'https://api.weixin.qq.com/sns/jscode2session',
							method: 'GET',
							data: {
								appid:'wxee7e0d5161c61923',
								secret:'0e32dd95e20b576d6de4e5df32778519',
								js_code:res.code,
								grant_type:'authorization_code'
							},
							success: res => {
								// console.log(res.data.openid)
								openid = res.data.openid
								
								//传到后端服务器。后端服务器需要判断是否已经登陆过，未登录则写入数据库，已经登陆过就直接返回登陆成功
								uni.request({
									url: serverUrl+'/wx_check_reg_yonghu-weixin.php',
									method: 'GET',
									data: {
										wx_openid: openid,
										wx_nicheng: nickName,
										wx_touxiang: avatarUrl
									},
									success: res => {
										// console.log(res.data)
										
										//写入缓存
										uni.setStorage({
										    key: 'wx_login',
										    data: 'ok',
										    success: function () {
										        console.log('写入缓存成功');
										    }
										});
										
										uni.setStorage({
										    key: 'wx_id',
										    data: res.data.uid,
										});
										
										uni.setStorage({
										    key: 'wx_nickName',
										    data: res.data.nickName,
										    success: function () {
												
												//跳转到首页
										        uni.switchTab({
										        	url: '/pages/index/index'
										        })
										    }
										});
									}
								});
							}
						});
					}
				});
			}
		}
	}
</script>

<style>
@import url("me.css");

</style>




<!-- 后台解密手机号 -->
<!-- https://www.cnblogs.com/dreamstartplace/p/10517356.html
https://www.cnblogs.com/zmdComeOn/p/11780173.html -->
<!-- <?php
namespace App\Http\Controllers\WxApplet;
 
use Illuminate\Http\Request;
use App\Http\Controllers\Controller;
use App\Repository\WxUserRepository;
 
include_once app_path('/Http/Controllers/WxApplet/Php/wxBizDataCrypt.php');
class WechatController extends Controller
{
  /**
   * constructer.
   *
   * @param WxUserRepository  $wxUser
   */
   public function __construct
   (
        WxUserRepository $WxUserRepository
   )
   {
        $this->WxUserRepository  = $WxUserRepository;
   }
    /**
     * 获取用户手机号码
     *
     * @return response
     */
    public function getWechatUserPhone(Request $request)
    {
        $code   =   $request->get('code');
        $encryptedData   =   $request->get('encryptedData');
        $iv   =  $request->get('iv');
        //小程序开发账户
        $appid  =  "*******" ;
        $secret =   "*******";
        $URL = "https://api.weixin.qq.com/sns/jscode2session?appid=$appid&secret=$secret&js_code=$code&grant_type=authorization_code";
        $apiData=file_get_contents($URL);
           if(!isset(json_decode($apiData)->errcode))
           {
              $sessionKey = json_decode($apiData)->session_key;
              $info = new \WXBizDataCrypt($appid, $sessionKey);
              $errCode = $info->decryptData($encryptedData, $iv, $data );
              if ($errCode == 0)
              {
                  $phone = json_decode($data)->phoneNumber;
                  $single_phone=$this->WxUserRepository->Single($phone);
                  if ($single_phone == null)
                  {
                     $wx_user = $this->WxUserRepository->Create($phone,$password);
                  }
                  return $this->Success(200003);
              }
              else {
                return $this->fail(420004);
             }
          }
    }
 } -->