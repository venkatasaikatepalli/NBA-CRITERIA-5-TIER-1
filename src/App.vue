  <template>
  <div id="app">
    <div class="header-top">
      <h1 class="text-center">PVP SIDDHARTHA INSTITUTE OF TECHNOLOGY</h1>
    </div>
    <nav class="navbar" role="navigation">
      <div class="container-fluid">
        <div class="navbar-header">
          <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-ex1-collapse">
            <span class="sr-only">Toggle navigation</span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
          </button>
          <a class="navbar-brand" href="#">NBA CRITERIA 5</a>
        </div>
        
        <!-- Collect the nav links, forms, and other content for toggling -->
        <div class="collapse navbar-collapse navbar-ex1-collapse">
          <ul class="nav navbar-nav navbar-right" v-if="!loginStatus">
            <li><router-link to="/">Home</router-link></li>
            <li><router-link to="/login">Login</router-link></li>
          </ul>
          <ul class="nav navbar-nav navbar-right" v-if="loginStatus">
            <li><router-link to="/dashboard">Dashboard</router-link></li>
            <li><router-link to="/forms">Forms</router-link></li>
            <li v-if="user_type === 'admin'"><router-link to="/roles">Roles</router-link></li>
            <li><router-link to="/reports">Reports</router-link></li>
            <li><a v-on:click="logout">Logout</a></li>
          </ul>
        </div><!-- /.navbar-collapse -->
      </div>
    </nav>
    <div class="container-fluid">
      <div class="row">
        <div class="col-md-12">
          <router-view @change="onLoginChange"></router-view>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
export default {
  data () {
    return {
      loginStatus: this.$store.getters.isAuthenticated,
      user_type: this.$store.getters.getUserType,
      head: true,
      mNav: false
    }
  },
  computed: {
    ...mapGetters([
      'isAuthenticated',
      'getUserDetails'
    ])
  },
  methods: {
    onLoginChange (value) {
      if (value.status === true) {
        this.loginStatus = value
      }
    },
    logout (event) {
      this.$store.dispatch('logout')
        .then(() => {
          this.loginStatus = false
          this.$router.push('/login')
        })
    }
  }
}
</script>

<style>
*{
  font-family: 'Quicksand', sans-serif;
  letter-spacing: 1px;
}
.header-top {
  padding: 1em 0em;
  background-color: rgba(37, 155, 193, 0.85);
  color: white;
}
.navbar {
  /*border:0;*/
  border-radius: 0px;
  /*margin-bottom: 0px;*/
  position: sticky;
  top: 0;
  background-color: black;
  z-index: 100;
}
.navbar-brand {
  color: white;
  font-weight: bold;
}
.nav>li>a {
  color: white;
  font-size: 0.9em;
}
.nav>li>a:hover, .nav>li>a:active, .nav>li>a:visited, .nav>li>a:focus {
  background-color: transparent;
}
</style>
