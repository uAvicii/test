<script>
import ContextMenu from '@/components/menu.vue'
export default {
  name: 'context-menu-view',
  components: {
    ContextMenu
  },
  data() {
    return {
      leftMenu: [
        { label: '部门' },
        { label: '员工' },
        { label: '角色' },
        { label: '权限' },
        { label: '领导' }
      ],
      leftSelected: '',
      rightMenu: [
        { label: '添加' },
        { label: '删除' },
        { label: '修改' },
        { label: '查看' },
        { label: '删除' }
      ],
      rightSelected: '',
      rightInnerMenu: [
        {
          label: '菜单1',
          subMenu: [{ label: '子菜单1' }, { label: '子菜单2' }, { label: '子菜单3' }]
        },
        { label: '菜单2' },
        { label: '菜单3' },
        { label: '菜单4' },
        { label: '菜单5' }
      ],
      rightInnerSelected: '',
      rightInnerSonMenu: [
        { label: '星期一' },
        { label: '星期二' },
        { label: '星期三' },
        { label: '星期四' },
        { label: '星期五' },
        { label: '星期六' },
        { label: '星期天' }
      ],
      rightInnerSonSelected: ''
    }
  }
}
</script>

<template>
  <div id="container">
    <ContextMenu
      :menu="leftMenu"
      @select="leftSelected = $event.label"
      style="flex: 1; margin-right: 30px"
    >
      <div id="left" style="overflow: hidden">
        <h1>{{ leftSelected }}</h1>
        <h2 class="title">
          <span>
            Migrating From MySQL to YugabyteDB Using YugabyteDB Voyager 
          </span>
        </h2>
      </div>
    </ContextMenu>

    <ContextMenu :menu="rightMenu" @select="rightSelected = $event.label" style="flex: 1">
      <div id="right" style="overflow: hidden">
        <h1>{{ rightSelected }}</h1>
        <ContextMenu :menu="rightInnerMenu" @select="rightInnerSelected = $event.label">
          <div id="right-inner" style="overflow: hidden">
            <h1>{{ rightInnerSelected }}</h1>
            <ContextMenu :menu="rightInnerSonMenu" @select="rightInnerSonSelected = $event.label">
              <div id="right-inner-son" style="overflow: hidden">
                <h1>{{ rightInnerSonSelected }}</h1>
              </div>
            </ContextMenu>
          </div>
        </ContextMenu>
      </div>
    </ContextMenu>
  </div>
</template>

<style scoped lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#container {
  width: 100vw;
  height: 100vh;
  display: flex;
}

#left {
  height: 50vh;
  background-color: skyblue;
  .title {
    color: #333;
    margin: 20px;
  }

  .title span {
    background: linear-gradient(to right, orange, hotpink) no-repeat right bottom;
    background-size: 0 2px;
    transition: background-size 1300ms;
  }
  .title span:hover {
    background-position-x: left;
    background-size: 100% 2px;
  }
}

#right {
  position: relative;
  box-sizing: border-box;
  height: 50vh;
  padding: 20px;
  background-color: greenyellow;
}

#right-inner {
  position: absolute;
  bottom: 20px;
  width: calc(100% - 40px);
  height: 200px;
  background-color: green;
}
#right-inner-son {
  position: absolute;
  bottom: 30px;
  width: calc(100% - 40px);
  height: 100px;
  margin: 20px;
  background-color: pink;
}
</style>
