<template>
	
	<div class="ui-app">
		
		<div class="time-banner">
			<div class="time-clock time" v-if="msTime.show">
				还剩: 
				<span class="day">{{msTime.day}}</span>
				天<span class="hour">{{msTime.hour}}</span>
				小时<span class="min">{{msTime.minutes}}</span>
				分<span class="sec">{{msTime.seconds}}</span>
				秒
			</div>
			<p class="over" v-show="over">活动已经结束</p>
		</div>

	</div>

</template>
<script>

	export default {
		replace:true,
		data () {
			return {
				msTime:{	//倒计时数值
					show:false,
					day:'',
					hour:'',
					minutes:'',
					seconds:''
				},
				star:'',	//活动开始时间
				end:'',		//活动结束时间
				nowClient:'', //客户端时间
				severClient:'',
				over:false	//结束状态
			}
		},
		props:{
			//时间控件ID
			id:{
				type: String,
				default :'1'
			},
			// 活动结束时间
		    endtime: {
		    	type: String
		    },
		    // 服务端时间,活动开始时间
		    servertime: {
		    	type: String
		    },
		    // 倒计时类型
		    type:{
		    	type:String,
		    	default:'avil'
		    }
		},
		compiled () {
			const self = this
			self.star = new Date(self.servertime).getTime()      
			self.end  = new Date(self.endtime).getTime()	     
			self.nowClient  = new Date().getTime()				

			console.log(self.star - self.nowClient)

			self.severClient = self.star - self.nowClient
			setTimeout(self.runTime,1)
		},
		methods: {
			runTime () {
				let timerID
				const self = this
				let msTime = self.msTime
				let timeDistance = ""
				let timeNow = ""
				timeNow = new Date().getTime()+ self.severClient
				timeDistance = self.end - timeNow
				if( timeDistance > 0 ){
					self.over = false
					self.msTime.show = true


					msTime.day = Math.floor( timeDistance / 86400000 )
					timeDistance-= msTime.day * 86400000
					msTime.hour = Math.floor( timeDistance / 3600000 )
					timeDistance-= msTime.hour * 3600000
					msTime.minutes = Math.floor( timeDistance / 60000 )
					timeDistance-= msTime.minutes * 60000
					msTime.seconds = new Number(timeDistance / 1000).toFixed(2)
					timeDistance-= msTime.seconds * 1000
			
					if( msTime.hour < 10){
						msTime.hour = "0" + msTime.hour
					}
					if(msTime.minutes < 10){
						msTime.minutes= "0" + msTime.minutes
					}
					if(msTime.seconds < 10) {
						msTime.seconds = "0" + msTime.seconds
					}
					setTimeout(self.runTime,1)
				}
				else {
					self.over = true
					self.msTime.show = false
				}
			}
		}
	}

</script>
<style>
	.time-banner {
	    position: relative;
	    float: left;
	}
	.time-banner .time-clock {
	    display: inline-block;
	}
    .time-banner .day,.time-banner .hour,.time-banner .min,.time-banner .sec {
	    padding: 0 3px
	}
	.time-banner .over{
		color: #ff0000
	}
</style>