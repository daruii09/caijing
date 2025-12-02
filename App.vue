<template>
	<view id="app">
		<!-- 应用入口 -->
	</view>
</template>

<script>
	import { token, userInfo } from '@/utils/storage'
	import { setToken, setUserInfo } from '@/store/index'
	import { loginApi } from '@/api/index'

	export default {
		onLaunch: function() {
			console.log('App Launch')
			// 初始化应用状态
			this.initApp()
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		},
		methods: {
			async initApp() {
				// 从本地存储恢复token和用户信息
				const tokenValue = token.get()
				const userInfoValue = userInfo.get()
				
				if (tokenValue) {
					setToken(tokenValue)
					
					// 如果有用户信息，恢复用户信息
					if (userInfoValue) {
						setUserInfo(userInfoValue)
					} else {
						// 如果没有用户信息，尝试获取
						try {
							const res = await loginApi.getUserInfo()
							if (res.data) {
								userInfo.set(res.data)
								setUserInfo(res.data)
							}
						} catch (error) {
							// 如果获取失败，清除token
							token.remove()
							setToken(null)
						}
					}
				}
			}
		}
	}
</script>

<style>
	/*每个页面公共css */
	@import './static/index.3e73f18a.css';
</style>

