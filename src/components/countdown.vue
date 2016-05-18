<template>
	
	<div class="ui-app">
		
		<div class="time-banner">
			<div class="time-clock time">
				还剩: 
				<span class="day">{{msTime.day}}</span>
				天<span class="hour">{{msTime.hour}}</span>
				小时<span class="min">{{msTime.minutes}}</span>
				分<span class="sec">{{msTime.seconds}}</span>
				秒
			</div>
		</div>

	</div>

</template>
<script>

	export default {
		replace:true,
		data () {
			return {
				msTime:{
					day:'',
					hour:'',
					minutes:'',
					seconds:''
				},
				star:'',
				end:'',
				nowClient:'',
				severClient:''
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
			self.star = new Date(self.servertime).getTime()      //活动开始时间
			self.end  = new Date(self.endtime).getTime()	     //活动结束时间
			self.nowClient  = new Date().getTime()				 //客户端时间
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
					msTime.day = Math.floor( timeDistance / 86400000 )
					timeDistance-= msTime.day * 86400000
					msTime.hour = Math.floor( timeDistance / 3600000 )
					timeDistance-= msTime.hour * 3600000
					msTime.minutes = Math.floor( timeDistance / 60000 )
					timeDistance-= msTime.minutes * 60000
					msTime.seconds = timeDistance / 1000 
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
					if(msTime.day==0&&msTime.hour==0&&msTime.minutes&&msTime.seconds){
					}
					setTimeout(self.runTime,1)
				}
				else if(timeDistance == 0){
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
</style>