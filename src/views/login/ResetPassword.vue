<!-- =========================================================================================
    File Name: ForgotPassword.vue
    Description: FOrgot Password Page
    ----------------------------------------------------------------------------------------
    Item Name: Vuexy - Vuejs, HTML & Laravel Admin Dashboard Template
      Author: Pixinvent
    Author URL: http://www.themeforest.net/user/pixinvent
========================================================================================== -->


<template>
    <div class="h-screen flex w-full bg-img">
        <div class="vx-col w-4/5 sm:w-4/5 md:w-3/5 lg:w-3/4 xl:w-3/5 mx-auto self-center">
            <vx-card>
                <div slot="no-body" class="full-page-bg-color">
                    <div class="vx-row">
                        <div class="vx-col hidden sm:hidden md:hidden lg:block lg:w-1/2 mx-auto self-center">
                            <img src="@/assets/images/pages/forgot-password.png" alt="login" class="mx-auto">
                        </div>
                        <div class="vx-col sm:w-full md:w-full lg:w-1/2 mx-auto self-center d-theme-dark-bg">
                            <div class="p-8">
                                <div class="vx-card__title mb-8">
                                    <h4 class="mb-4">Asignar Nuevo  password</h4>
                                    <p>Por favor ingrese su nuevo password.</p>
                                </div>

                                <vs-input 
                                    type="password"
                                    label-placeholder="new password" 
                                    v-model="password" 
                                    v-validate="'required|min:6|max:10'"
                                    class="w-full mb-8" />
                                <vs-button type="border" to="/login" class="px-4 w-full md:w-auto"> Login</vs-button>
                                <vs-button 
                                    class="float-right px-4 w-full md:w-auto mt-3 mb-8 md:mt-0 md:mb-0"
                                    :disabled="!validateForm" 
                                    @click="forgotPassword()" 
                                    >Nuevo  Password</vs-button>
                            </div>
                        </div>
                    </div>
                </div>
            </vx-card>
        </div>
    </div>
</template>

<script>
import router from '@/router'
export default {
  data () {
    return {
      password: ''
    }
  },
  computed: {
     validateForm () {
      // && this.password !== '' && this.confirm_password !== '' && this.isTermsConditionAccepted === true
      return !this.errors.any()  && this.password !== ''
    }
  },
   methods: {
      forgotPassword(){
         
        this.$store.dispatch('auth/resetPassword', this.password).then((msg)=>{

            if(msg.data.success){
                this.$vs.notify({
                    time:4000,
                    title:'PASSWORD',
                    text:'Su password se actualizo con exito ..',
                    color:'success',
                    iconPack: 'feather',
                    icon: 'icon-clock'
                })     
                
                router.push(router.currentRoute.query.to || '/login')
                  
            }
        })

      }
  }
}
</script>
