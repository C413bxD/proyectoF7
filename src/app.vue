<template>
  <!-- App -->
  <f7-app :params="f7params" >

    <!-- Statusbar -->
    <f7-statusbar></f7-statusbar>

    <!-- Left Panel -->
    <f7-panel left reveal>
      <f7-view url="/panel-left/"></f7-view>
     
      
      
    </f7-panel>

    <!-- Right Panel -->
    <f7-panel right cover>
      <f7-view url="/panel-right/"></f7-view>
    </f7-panel>

    <!-- Main View -->
    <f7-view  id="main-view" url="/" main></f7-view>

    <!-- Popup -->
    <f7-popup theme-dark id="popup">
      <f7-view>
        <f7-page>
          <f7-navbar title="Popup">
            <f7-nav-right>
              <f7-link popup-close>Cerrar</f7-link>
            </f7-nav-right>
          </f7-navbar>
          <f7-block>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Neque, architecto. Cupiditate laudantium rem nesciunt numquam, ipsam. Voluptates omnis, a inventore atque ratione aliquam. Omnis iusto nemo quos ullam obcaecati, quod.</f7-block>
        </f7-page>
      </f7-view>
    </f7-popup>

    <!-- Login Screen -->
    <f7-login-screen id="login-screen">
      <f7-view>
        <f7-page login-screen>
          <f7-login-screen-title>Login</f7-login-screen-title>
          <f7-list form>
            <f7-list-item>
              <f7-label>Username</f7-label>
              <f7-input name="username" placeholder="Username" type="text"></f7-input>
            </f7-list-item>
            <f7-list-item>
              <f7-label>Password</f7-label>
              <f7-input name="password" type="password" placeholder="Password"></f7-input>
            </f7-list-item>
          </f7-list>
          <f7-list>
            <f7-list-button @click="firebaseLogin" title="Sign In" ></f7-list-button>
            <!-- <login-screen-close> -->
            <f7-block-footer>
              <p>Click Sign In to close Login Screen</p>
            </f7-block-footer>
          </f7-list>
        </f7-page>
      </f7-view>
    </f7-login-screen>

  </f7-app>
</template>

<script>
// Import Routes
import routes from './routes.js'
import firebase from 'firebase';
export default {
  data() {
    return {
      // Framework7 parameters here
      f7params: {
        id: 'io.framework7.testapp', // App bundle ID
        name: 'Framework7', // App name
        theme: 'auto', // Automatic theme detection
        // App routes
        routes: routes,
      },
      form: {
        email: 'antony@mail.com',
        password: '1234679',
      },
      error:''
    }
  },
  methods:{
    firebaseLogin(){
      this.error = ''
      if(this.form.email && this.form.password){
        return firebase.auth().signInWithEmailAndPassword(this.form.email, this.form.password)
      .then(()=>{
        //this.$router.push({name:'muestra'})
        console.log('Registrado')
      }).catch(err=>{
        this.error = err.message
      })
      }
      else {
        this.error = "Todos los campos son requeridos"
      }
      
    },
  }
}
</script>
