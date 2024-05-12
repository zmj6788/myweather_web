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
                  <a-menu @click="myCity">
                    <a-menu-item key="zhengzhou">
                      <a href="javascript:;">郑州</a>
                    </a-menu-item>
                    <a-menu-item key="beijing">
                      <a href="javascript:;">北京</a>
                    </a-menu-item>
                    <a-menu-item key="shanghai">
                      <a href="javascript:;">上海</a>
                    </a-menu-item>
                  </a-menu>
                </template>
              </a-dropdown>
            </a-breadcrumb-item>
            <a-breadcrumb-item>
              <a-input-search v-model:value="value" placeholder="搜索城市" style="width: 200px" @search="onSearch" />
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

      <main>
        <div class="today">
          <div class="today_weather">

            <a-breadcrumb>
              <a-breadcrumb-item>
                <div class="message_weather">
                  <div style="background: #87c0ca; padding: 30px">
                    <a-card title="温度 晴" :bordered="false" 
                      style="background: #87c0ca; width: 300px">
                      <p>风向 风级</p>
                      <p>天气指数：</p>
                      <p>湿度：</p>
                    </a-card>

                  </div>
                </div>
              </a-breadcrumb-item>
              <a-breadcrumb-item>
                <div class="img_weather">
                  <img alt="example" :src="qing" />

                </div>
              </a-breadcrumb-item>
            </a-breadcrumb>
          </div>
        </div>
        <div class="week">
          <div class="week_weather">
            <a-card title="一周内天气" style="background: #87c0ca;">
              <a-card-grid style=" width: 25%; height:125px; text-align: center">
                <h1>日期</h1>
                <p>天气</p>
              </a-card-grid>
              <a-card-grid style="width: 25%; text-align: center">Content</a-card-grid>
              <a-card-grid style="width: 25%; text-align: center">Content</a-card-grid>
              <a-card-grid style="width: 25%; text-align: center">Content</a-card-grid>
              <a-card-grid style="width: 25%;  height:125px; text-align: center">Content</a-card-grid>
              <a-card-grid style="width: 25%; text-align: center">Content</a-card-grid>
              <a-card-grid style="width: 25%; text-align: center">Content</a-card-grid>
              <a-card-grid style="width: 25%; text-align: center">Content</a-card-grid>
            </a-card>
          </div>
        </div>
      </main>
    </div>
  </div>

</template>
<script setup>
import qing from '@/assets/images/qing.jpg';
import { onMounted } from 'vue';
let cityName = "郑州"
const cityweather = {
  cityName: "",
  temperature: "",
  info: "",
  direct: "",
  power: "",
  aqi: "",
  humidity: "",
  weekWeather: []
}
// 获取天气信息
const getWeather = () => {

  $.ajax({
    url: "http://myweather.com/api/weather",
    type: "GET",
    data: { city: cityName }, // 这里直接传递对象，jQuery会自动处理为查询字符串
    success: function (res) {
      console.log(res);
      const { data } = res;
      cityweather.cityName = data.City;
      cityweather.temperature = data.Temperature;
      cityweather.info = data.Info;
      cityweather.direct = data.Direct;
      cityweather.power = data.Power;
      cityweather.aqi = data.Aqi;
      cityweather.humidity = data.Humidity;
      cityweather.weekWeather = data.WeatherWeek;
      console.log(cityweather);
      console.log(cityweather.weekWeather[0]);
[0]    }
  });
};

//城市匹配
const myCity = (key) => {
  switch (key.key) {
    case 'zhengzhou':
      cityName = "郑州";
      getWeather();
      break;
    case 'beijing':
      cityName = "北京";
      getWeather();
      break;
    case 'shanghai':
      cityName = "上海";
      getWeather();
      break;
  }
};

//渲染天气数据

onMounted(() => {
  // 确保DOM已经挂载完成后再操作
  getWeather();
  const messageWeather = document.querySelector(".message_weather")
  console.log(messageWeather);
  
});


</script>

<style lang="scss">
.myweather {
  width: 100%;
  height: 100vh;

  .main {

    header {
      width: 100%;
      height: 90px;
      background-color: #108b96;
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

        img {
          width: 40px;
          height: 40px;
          border-radius: 50%;
          margin-right: 20px;
        }
      }

    }

    main {
      width: 100%;
      height: calc(100vh - 90px);
      background-color: #5aa4ae;

      .today {
        padding: 10px 80px;
      }

      .today_weather {
        background-color: #87c0ca;
        display: flex;
        justify-content: center;
      }

      .message_weather {
        margin-right: 300px;
      }

      .img_weather {
        width: 300px;
        height: 210px;
        margin-top: 30px;
        display: flex;
        justify-content: center;
        /* 水平居中 */
        align-items: center;

        /* 垂直居中 */
        img {
          width: 200px;
          height: 200px;
        }
      }

      .week {
        padding: 10px 80px;
      }
    }
  }
}
</style>