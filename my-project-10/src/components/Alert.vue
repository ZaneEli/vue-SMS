<!-- 添加新用户成功后弹窗 -->

<template>
	<!-- 弹窗html https://www.bootcss.com/ 组件中找到弹窗代码 贴过来即可 -->
  	<div class="alert alert-warning alert-dismissible" role="alert">
	<button type="button" class="close" data-dismiss="alert" aria-label="Close"><span aria-hidden="true">&times;</span></button>
	{{message}}
	</div>
</template>

<script>
export default {
  name: 'alert',
  props:["message"],
  data () {
    return {
      
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
