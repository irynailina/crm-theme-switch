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
                    <ul class="ml-auto navbar-nav header-menu ">
                            <li class="nav-item">
                            <a @click="$bvModal.show('ThemeModal')" class="add-summary nav-link">
                                <i class="fas fa-cog"></i>
                            </a>
                        </li>

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
          <theme-modal></theme-modal>
        </div><!-- /.main-wrap -->
    </div><!-- /.page-container -->
    </div>
</template>

<script>
import NewEmployeeModal from '@/components/NewEmployeeModal'
import SideBar from '@/components/SideBar'
import ThemeModal from '@/components/ThemeModal'
export default {
  name: 'BaseContainer',
  components: {
    'new-employee-modal': NewEmployeeModal,
    'side-bar': SideBar,
    'theme-modal': ThemeModal
  },
  data: function () {
    return {
      showSidebar: false,
      moveSidebar: false,
      isClosed: false
    }
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
