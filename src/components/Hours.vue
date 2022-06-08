<template>
<span>{{sday}}</span>
</template>
<script>
import dayjs from 'dayjs'
export default {
    time(){
        this.timeId = setInterval(()=>{
   this.sday =dayjs().format('YYYY-MM-DD HH:mm:ss');

}, 1000);
    }
};
</script>
<style lang="scss" scoped>
 
</style>