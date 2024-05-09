<script>
</script>

<template>

  <div class="myweather">
    <div class="main">

      <header>
        <div class="logo">
          <div>我的天气</div>
          <div>myweather</div>
        </div>
        <div class="left">
          <a-breadcrumb separator="">
            <a-breadcrumb-item>首页</a-breadcrumb-item>
            <a-breadcrumb-item>当前城市</a-breadcrumb-item>
            <a-breadcrumb-item>
              <a-dropdown>
                <a class="ant-dropdown-link" @click.prevent>
                  我的城市
                  <i class="fa fa-chevron-down"></i>
                </a>
                <template #overlay>
                  <a-menu>
                    <a-menu-item>
                      <a href="javascript:;">郑州</a>
                    </a-menu-item>
                    <a-menu-item>
                      <a href="javascript:;">北京</a>
                    </a-menu-item>
                    <a-menu-item>
                      <a href="javascript:;">焦作</a>
                    </a-menu-item>
                  </a-menu>
                </template>
              </a-dropdown>
            </a-breadcrumb-item>
            <a-breadcrumb-item>
                <a-input-search v-model:value="value" placeholder="搜索城市" style="width: 200px"@search="onSearch" />
            </a-breadcrumb-item>
          </a-breadcrumb>
        </div>
        <div class="right">
          <img src="https://q.qlogo.cn/g?b=qq&nk=2124427385&s=100" alt="">
          <a-dropdown>
            <a class="ant-dropdown-link" @click.prevent>
              用户名
              <i class="fa fa-chevron-down"></i>
            </a>
            <template #overlay>
              <a-menu>

                <a-menu-item>
                  <a href="javascript:;">退出登录</a>
                </a-menu-item>
              </a-menu>
            </template>
          </a-dropdown>
        </div>
      </header>
      <div class="tabs">

      </div>
      <main>

      </main>
    </div>
  </div>

</template>

<style lang="scss">
.myweather {
  width: 100%;
  height: 100vh;

  .main {

    header {
      width: 100%;
      height: 90px;
      background-color: #649bf6;
      display: flex;
      justify-content: space-between;
      align-items: center;

      .logo {
        width: 10%;
        transform: scale(0.9);
        margin-left: 100px;

        div:first-child {
          font-size: 26px;
        }

        div:last-child {
          font-size: 19px;
        }
      }

      .left {
        width: 50%;
        display: flex;
        margin-left: 40px;

        span {
          margin-right: 30px;
        }

        .search i {
          cursor: pointer;
        }
      }

      .right {
        width: 40%;
        margin-right: 100px;
        display: flex;
        justify-content: right;
        align-items: center;

        img{
          width: 40px;
          height: 40px;
          border-radius: 50%;
          margin-right: 20px;
        }
      }

    }
  }
}
</style>