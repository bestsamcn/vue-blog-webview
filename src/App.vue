<style src="./assets/css/common/base.css"></style>
<template>
    <div id="app">
        <Loading :is-loading="iShowLoading"></Loading>
        <transition enter-active-class="animated fadeIn" leave-active-class="animated fadeOut">
        <Toast :msg="toastMsg" v-show="iShowToast"></Toast>
        </transition>
        <keep-alive>
            <router-view class="router-view"></router-view>
        </keep-alive>
    </div>
</template>

<script>
import './assets/libs/animate.css/animate.min.css';
import './assets/libs/Font-Awesome-3.2.1/css/font-awesome.min.css';
import { mapState, mapActions } from 'vuex';
import Loading from './components/common/loading.vue';
import Toast from './components/common/toast.vue';


export default {
    name: 'app',
    data(){
        return{
            isResizeToMobile:false
        }
    },
    components:{
        Loading,
        Toast,
    },
    computed:{
        ...mapState({
            iShowLoading:state=>state.common.iShowLoading,
            iShowMenu:state=>state.common.iShowMenu,
            iShowToast:state=>state.common.iShowToast,
            toastMsg:state=>state.common.toastMsg,
            routerName:state=>state.RouteModule.name
        })
    },
    methods:{
        ...mapActions([
            'setToast'
        ]),
        onLogoClick(e){
            this.setToast(e);
        },
        onresizeWindow(){
            var cw = document.documentElement.clientWidth || document.body.clientWidth;
            if(cw >= 768){
                this.isResizeToMobile = false;
            }else{
                this.isResizeToMobile = true;
            }
        }
    },
    created(){
        window.addEventListener('resize', this.onresizeWindow);
        window.addEventListener('load', this.onresizeWindow);
    }
    
   
}
</script>

