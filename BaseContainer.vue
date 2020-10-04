<template>
    <div style="display: flex;width: 100%;" v-bind:class="{'adaptive': isClosed}">
<side-bar @close-side="closeSide" :showSidebar="showSidebar">
</side-bar>
<div :class="{'page-container-move': moveSidebar}" class="page-container">
        <div class="main-wrap">
            <!-- header -->
            <header>
                <nav class="navbar navbar-expand-sm bg-dark-team navbar-dark">
                    <button type="button" @click="sidebarOpen" class="btn-sidebar">
                        <i class="fas fa-align-left"></i>
                    </button>
<!-- theme -->
                       <div class="theme-switch">
              <svg
                aria-hidden="true"
                data-prefix="fas"
                data-icon="sun"
                role="img"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 512 512"
                class="theme-switch__icon"
              >
                <path
                  fill="currentColor"
                  d="M256 160c-52.9 0-96 43.1-96 96s43.1 96 96 96 96-43.1 96-96-43.1-96-96-96zm246.4 80.5l-94.7-47.3 33.5-100.4c4.5-13.6-8.4-26.5-21.9-21.9l-100.4 33.5-47.4-94.8c-6.4-12.8-24.6-12.8-31 0l-47.3 94.7L92.7 70.8c-13.6-4.5-26.5 8.4-21.9 21.9l33.5 100.4-94.7 47.4c-12.8 6.4-12.8 24.6 0 31l94.7 47.3-33.5 100.5c-4.5 13.6 8.4 26.5 21.9 21.9l100.4-33.5 47.3 94.7c6.4 12.8 24.6 12.8 31 0l47.3-94.7 100.4 33.5c13.6 4.5 26.5-8.4 21.9-21.9l-33.5-100.4 94.7-47.3c13-6.5 13-24.7.2-31.1zm-155.9 106c-49.9 49.9-131.1 49.9-181 0-49.9-49.9-49.9-131.1 0-181 49.9-49.9 131.1-49.9 181 0 49.9 49.9 49.9 131.1 0 181z"
                ></path>
              </svg>

              <div class="switch">
                <input
                  class="switch__input js-switch-input"
                  type="checkbox"
                  name="theme"
                  id="theme-switch-control"
                  @change="lightMode = !lightMode"
                />
                <label
                  aria-hidden="true"
                  class="switch__label"
                  for="theme-switch-control"
                  >On</label
                >
                <div aria-hidden="true" class="switch__marker"></div>
              </div>

              <svg
                aria-hidden="true"
                data-prefix="fas"
                data-icon="moon"
                role="img"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 512 512"
                class="theme-switch__icon"
              >
                <path
                  fill="currentColor"
                  d="M283.211 512c78.962 0 151.079-35.925 198.857-94.792 7.068-8.708-.639-21.43-11.562-19.35-124.203 23.654-238.262-71.576-238.262-196.954 0-72.222 38.662-138.635 101.498-174.394 9.686-5.512 7.25-20.197-3.756-22.23A258.156 258.156 0 0 0 283.211 0c-141.309 0-256 114.511-256 256 0 141.309 114.511 256 256 256z"
                ></path>
              </svg>
            </div>
                    <!-- <ThemeSwitcher /> -->
                    <ul class="ml-auto navbar-nav header-menu ">
                        <li class="nav-item">
                            <a @click="$bvModal.show('newEmployeeModal')" class="add-summary nav-link">
                                <i class="fas fa-plus"></i>
                            </a>
                        </li>
                        <li class="nav-item users">
                            <a class="nav-link"><i class="fas fa-user-alt"></i>
                                <div class="d-inline-block">
                                    <span class="c-light-blue-500">{{$store.state.userName}}</span>
                                </div>
                            </a>
                        </li>
                    </ul>
                </nav>
            </header>
            <slot></slot>
          <new-employee-modal></new-employee-modal>
        </div><!-- /.main-wrap -->
    </div><!-- /.page-container -->
    </div>
</template>

<script>
import NewEmployeeModal from '@/components/NewEmployeeModal'
import SideBar from '@/components/SideBar'
// import ThemeSwitcher from '@/components/ThemeSwitcher'
export default {
  name: 'BaseContainer',
  components: {
    'new-employee-modal': NewEmployeeModal,
    'side-bar': SideBar
    // ThemeSwitcher
  },
  data: function () {
    return {
      showSidebar: false,
      moveSidebar: false,
      isClosed: false,
      lightMode: false
    }
  },
  watch: {
    lightMode: function () {
      localStorage.setItem('lightMode', JSON.stringify(this.lightMode))
      window.eventBus.$emit('changeLightMode', this.lightMode)
    }
  },
  created () {
    this.lightMode = JSON.parse(localStorage.getItem('lightMode'))
  },
  methods: {
    sidebarOpen () {
      this.showSidebar = !this.showSidebar
      this.moveSidebar = !this.moveSidebar
      this.isClosed = true
      this.setLocalState()
    },
    closeSide () {
      this.isClosed = false
      this.showSidebar = false
      localStorage.setItem('isClosed', this.isClosed)
      localStorage.setItem('showSidebar', this.showSidebar)
    },
    setLocalState () {
      localStorage.setItem('showSidebar', this.showSidebar)
      localStorage.setItem('moveSidebar', this.moveSidebar)
      localStorage.setItem('isClosed', this.isClosed)
    }
  },
  mounted () {
    if (localStorage.getItem('showSidebar') === 'true') {
      this.showSidebar = localStorage.getItem('showSidebar')
    }
    if (localStorage.getItem('moveSidebar') === 'true') {
      this.moveSidebar = localStorage.getItem('moveSidebar')
    }
    if (localStorage.getItem('isClosed') === 'true') {
      this.isClosed = localStorage.getItem('isClosed')
    }
  }
}
</script>
