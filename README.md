# vue-countdown

## [Live demo](http://andylei18.github.io/vue-countdown/)

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:9999
npm run dev

# build for production with minification
npm run build

# Options
* :endtime      String
* :id           String
* :servertime	String
* callback      Function




# countdown.vue


<template>
	
	<count-down :endtime="time.endtime" :id="time.id" :servertime="time.servertime"></count-down>

</template>

