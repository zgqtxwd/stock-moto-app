<template>
    <f7-page>
        <f7-navbar>
            <f7-nav-left>
                <f7-link class="panel-open" open-panel="left" icon="fa fa-bars"></f7-link>
            </f7-nav-left>
            <div class="title">Stock Moto</div>
            <f7-nav-right>
                <f7-link>
                    <f7-icon icon="fa fa-bell-o">
                        <f7-badge color="red">5</f7-badge>
                    </f7-icon>
                </f7-link>
                <f7-link popover-open=".popover-menu">
                    <img :src="user ? user.avatarUrl : ''" :alt="user.fullName"
                         class="avatar-upload br-100 user-avatar">
                </f7-link>
            </f7-nav-right>
        </f7-navbar>

        <f7-block>
            <f7-row>
                <f7-col @click.native="goToPage('/sales/')">
                    <f7-card>
                        <f7-card-content>
                            <div class="img-circular" style="background-image: url('http://i.pravatar.cc/110')"></div>
                            <f7-block-title class="text-align-center mt-1">Sales</f7-block-title>
                        </f7-card-content>
                    </f7-card>
                </f7-col>
                <f7-col @click.native="goToPage('/products/')">
                    <f7-card>
                        <f7-card-content>
                            <div class="img-circular" style="background-image: url('http://i.pravatar.cc/109')"></div>
                            <f7-block-title class="text-align-center mt-1">Buys</f7-block-title>
                        </f7-card-content>
                    </f7-card>
                </f7-col>
            </f7-row>
            <f7-row>
                <f7-col @click.native="goToPage('/staffs/')">
                    <f7-card>
                        <f7-card-content>
                            <div class="img-circular" style="background-image: url('http://i.pravatar.cc/101')"></div>
                            <f7-block-title class="text-align-center mt-1">Staffs</f7-block-title>
                        </f7-card-content>
                    </f7-card>
                </f7-col>
                <f7-col @click.native="goToPage('/reports')">
                    <f7-card>
                        <f7-card-content>
                            <div class="img-circular" style="background-image: url('http://i.pravatar.cc/102')"></div>
                            <f7-block-title class="text-align-center mt-1">Reports</f7-block-title>
                        </f7-card-content>
                    </f7-card>
                </f7-col>
            </f7-row>
            <f7-row>
                <f7-col @click.native="goToPage('/expenses')">
                    <f7-card>
                        <f7-card-content>
                            <div class="img-circular" style="background-image: url('http://i.pravatar.cc/103')"></div>
                            <f7-block-title class="text-align-center mt-1">Expenses</f7-block-title>
                        </f7-card-content>
                    </f7-card>
                </f7-col>
                <f7-col @click.native="goToPage('/customers')">
                    <f7-card>
                        <f7-card-content>
                            <div class="img-circular" style="background-image: url('http://i.pravatar.cc/150')"></div>
                            <f7-block-title class="text-align-center mt-1">Customers</f7-block-title>
                        </f7-card-content>
                    </f7-card>
                </f7-col>
            </f7-row>
        </f7-block>
        <f7-popover class="popover-menu">
            <f7-list>
                <f7-list-item link="/account/" popover-close title="Account">
                    <f7-icon slot="media" icon="fa fa-user"></f7-icon>
                </f7-list-item>
                <f7-list-item link="#" popover-close title="Setting">
                    <f7-icon slot="media" icon="fa fa-wrench"></f7-icon>
                </f7-list-item>
                <f7-list-item link="#" popover-close title="Language">
                    <f7-icon slot="media" icon="fa fa-language"></f7-icon>
                </f7-list-item>
                <f7-list-item link="#" popover-close title="Logout" @click.native="logout">
                    <f7-icon slot="media" icon="fa fa-unlock"></f7-icon>
                </f7-list-item>
            </f7-list>
        </f7-popover>
    </f7-page>
</template>
<script>
  export default {
    name: 'HomePage',
    computed: {
      user: {
        get () {
          if (this.$store.state.auth.user) {
            return this.$store.state.auth.user
          }
          return { avatarUrl: '' }
        }
      }
    },
    methods: {
      goToPage (page) {
        this.$f7router.navigate(page)
      },
      logout () {
        this.$store.dispatch('auth/logout')
      }
    },
    watch: {
      '$store.state.auth': {
        deep: true,
        immediate: true,
        handler (value) {
          if (!value.authenticated) {
            const self = this
            self.$f7router.refreshPage()
          }
        }
      }
    }
  }

</script>
