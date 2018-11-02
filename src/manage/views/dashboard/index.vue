<template>
  <div class="dashboard-container">
    <component :is="currentRole"/>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import adminDashboard from './admin'
import managerDashboard from './manager'
import salesDashboard from './sales'
import operatorDashboard from './operator'
import acountantDashboard from './accountant'
import sponsorDashboard from './sponsor'
import channelDashboard from './channel'
//import store from '../store'
export default {
    name: 'Dashboard',
    components: {
        adminDashboard,
        managerDashboard,
        salesDashboard,
        operatorDashboard,
        acountantDashboard,
        sponsorDashboard,
        channelDashboard
    },
    data() {
    return {

            currentRole: 'adminDashboard'
    }
    },
    computed: {
        ...mapGetters([
            'roles','status','loginState','setting'
        ])
    },
    watch: {
        loginState() {
            //console.log('我的角色99999=' + this.loginState.userInfo.group.name)
             console.log('我的loginstate='+JSON.stringify(this.loginState.userInfo));
            // if (this.loginState.userInfo.group.name.includes('超级管理员')) {
            //     this.currentRole = 'adminDashboard2'
            // }
            var rolesg=this.loginState.userInfo.group.name
            switch(rolesg)
            {
                case '管理':
                    this.currentRole = 'managerDashboard'
                    break;
                case '销售':
                    this.currentRole = 'salesDashboard'
                    break;
                case '运营':
                    this.currentRole = 'operatorDashboard'
                    break;
                case '财务':
                    this.currentRole = 'accountantDashboard'
                    break;
                case '广告主':
                    this.currentRole = 'sponsorDashboard'
                    break;
                case '渠道':
                    this.currentRole = 'channelDashboard'
                    break;
                default:
                    this.currentRole = 'adminDashboard'
            }
        }
    },
    mounted() {
         this.$store.dispatch("loginState", { })
    },
    created() {

    }
}
</script>
