<template>
  <div class="home">
    <van-row class="my-title">
      <van-col span="8" class="my-col-one"><van-icon name="cross" /></van-col>
      <van-col span="8" class="my-col-two">贷款大全</van-col>
      <van-col span="8" class="my-col-three"><van-icon name="ellipsis" /></van-col>
    </van-row>
    <div class="my-top"></div>
    <van-notice-bar
      text="同时申请3款以上产品，下款率可达90%以上"
      left-icon="warning"
      right-icon='close'
      background='#ffedcc'
      mode="closeable"
      @close='closeBar'
      :speed='50'
      scrollable
    />
    <van-search 
      placeholder="输入搜索内容" 
      v-model="val" 
      input-align='center'
    />
    <van-dropdown-menu active-color='#FA5151'>
      <van-dropdown-item title="类型" ref="item">
        <van-row type="flex" justify="space-around" class="my-drop1">
          <van-col 
            span="6" 
            class="my-col"
            v-for="(item, index) in arrVal"
            :key="index"
            :class="{'bac':item.isCheck}"
            @click.native="myChange(item.id)"
          >{{item.text}}</van-col>
        </van-row>
      </van-dropdown-item>
      <van-dropdown-item title="额度" ref="item2">
        <van-row gutter="20" class="my-drop2">
          <van-col 
            span="8" 
            class="my-col"
            v-for="(item, index) in arrVal2"
            :key="index"
            :class="{'bac':item.isCheck}"
            @click.native="myChange2(item.id)"
          >{{item.text}}</van-col>
        </van-row>
      </van-dropdown-item>
      <van-dropdown-item title="周期" ref="item3">
        <van-row gutter="20" class="my-drop3">
          <van-col 
            span="8" 
            class="my-col"
            v-for="(item, index) in arrVal3"
            :key="index"
            :class="{'bac':item.isCheck}"
            @click.native="myChange3(item.id)"
          >{{item.text}}</van-col>
        </van-row>
        <div class="my-button">
          <van-button square @click="onConfirm">取消</van-button>
          <van-button square @click="onConfirm">确认</van-button>
        </div>
      </van-dropdown-item>
      <van-dropdown-item v-model="value" :options="option" />
    </van-dropdown-menu>
    <van-tabs>
      <van-tab v-for="item in title" :title="item" />
    </van-tabs>
    <div class="my-list" v-for="(index) in 4" :key="index">
      <van-row gutter="20" class="my-list-row">
        <van-col span="4"><img src="@/assets/images/list.jpg" alt="" class="my-img"></van-col>
        <van-col span="12">
          <div class="my-username">
            <span class="my-one">小花钱包</span>
            <span class="my-two">额度高</span>
          </div>
          <div class="my-tip">随借随还，方便灵活</div>
        </van-col>
        <van-col span="8" class="my-t">4.4万人已申请</van-col>
      </van-row>
      <van-row class="my-list-row2">
        <van-col span="7" class="my-one">
          <div class="my-ti">5000-2万</div>
          <div class="my-ti2">额度范围(元)</div>
        </van-col>
        <van-col span="11" class="my-two">
          <div class="my-ti">月利息：2.3%</div>
          <div class="my-ti2">还款周期：1-36个月</div>
        </van-col>
        <van-col span="6" class="my-three">
          <van-button round size="small">立即申请</van-button>
        </van-col>
      </van-row>
    </div>
    <div class="my-scope"> </div>
    <van-tabbar v-model="active">
      <van-tabbar-item icon="home-o">首页</van-tabbar-item>
      <van-tabbar-item icon="search">贷款大全</van-tabbar-item>
      <van-tabbar-item icon="friends-o">优质贷款</van-tabbar-item>
      <van-tabbar-item icon="setting-o">我的</van-tabbar-item>
    </van-tabbar>
  </div>
</template>

<script>
import { setTimeout } from 'timers';

export default {
  name: 'home',
  data() {
    return {
      val: '',
      value: 0,
      active: 0,
      option: [
        { text: '最新上架', value: 0 },
        { text: '下款率由高到低', value: 1 },
        { text: '下款额度由高到低', value: 2 },
        { text: '申请人数由高到低', value: 3 }
      ],
      arrVal: [
        { text: '最新上架', id: 0, isCheck: false },
        { text: '通过率高', id: 1, isCheck: false },
        { text: '申请人数', id: 2, isCheck: false },
        { text: '平均金额', id: 3, isCheck: false }
      ],
      arrVal2: [
        { text: '5000以下', id: 0, isCheck: false },
        { text: '5000-10000', id: 1, isCheck: false },
        { text: '10000-30000', id: 2, isCheck: false },
        { text: '30000以上', id: 3, isCheck: false }
      ],
      arrVal3: [
        { text: '1-15天', id: 0, isCheck: false },
        { text: '15-30天', id: 1, isCheck: false },
        { text: '1-3个月', id: 2, isCheck: false },
        { text: '3-6个月', id: 3, isCheck: false },
        { text: '6-12个月', id: 4, isCheck: false },
        { text: '12个月以上', id: 5, isCheck: false },
      ],
      title: [ '本周放款王', '手机号贷', '身份证贷', '身份证贷', '银行卡贷'],
    }
  },
  methods: {
    closeBar() {},
    onConfirm() {
      this.$refs.item3.toggle();
    },
    myChange(id) {
      this.arrVal.forEach(item => {
        item.isCheck = false;
      })
      this.arrVal[id]['isCheck'] = true;
      setTimeout(() => {
        this.$refs.item.toggle();
      }, 400);
    },
    myChange2(id) {
      this.arrVal2.forEach(item => {
        item.isCheck = false;
      })
      this.arrVal2[id]['isCheck'] = true;
      setTimeout(() => {
        this.$refs.item2.toggle();
      }, 400);
    },
    myChange3(id) {
      this.arrVal3.forEach(item => {
        item.isCheck = false;
      })
      this.arrVal3[id]['isCheck'] = true;
    }
  },
}
</script>

<style lang="scss" scoped>
.home {
  .my-title {
    position: fixed;
    top: 0;
    width: 100%;
    z-index: 10;
    background-color: #f2f2f2;
    line-height: 1rem;
    font-weight: 700;
    .my-col-one {
      font-size: 0.5rem;
      padding-left: 0.3rem;
    }
    .my-col-two {
      font-size: 0.45rem;
      text-align: center;
    }
    .my-col-three {
      padding-right: 0.3rem;
      font-size: 0.5rem;
      text-align: right;
    }
  }
  .my-top {
    width: 100%;
    height: 0.99rem;
  }
  .my-drop1 {
    padding: 0.5rem 0;
    .my-col {
      font-size: 0.4rem;
      line-height: 0.8rem;
      text-align: center;
      border-radius:2px;
      width: 2rem;
      color: #ccc;
      border:1px solid rgba(204,204,204,1);
    }
    .my-col.van-col.van-col--6.bac {
      background:linear-gradient(90deg,rgba(249,97,84,1) 0%,rgba(247,130,98,1) 100%);
      color: #fff;
    }
  }
  .my-drop2 {
    padding: 0.5rem 0.5rem;
    .my-col {
      margin-left: 0.1rem;
      font-size: 0.4rem;
      line-height: 0.8rem;
      text-align: center;
      border-radius:2px;
      width: 3rem;
      color: #ccc;
      border:1px solid rgba(204,204,204,1);
      padding: 0px !important;
      &:last-of-type {
        margin-top: 0.2rem;
      }
    }
    .my-col.van-col.van-col--8.bac {
      background:linear-gradient(90deg,rgba(249,97,84,1) 0%,rgba(247,130,98,1) 100%);
      color: #fff;
    }
  }
  .my-drop3 {
    padding: 0.5rem 0.5rem;
    .my-col {
      margin-left: 0.1rem;
      font-size: 0.4rem;
      line-height: 0.8rem;
      text-align: center;
      border-radius:2px;
      width: 3rem;
      color: #ccc;
      border:1px solid rgba(204,204,204,1);
      padding: 0px !important;
      &:nth-child(n+4) {
        margin-top: 0.2rem;
      }
    }
    .my-col.van-col.van-col--8.bac {
      background:linear-gradient(90deg,rgba(249,97,84,1) 0%,rgba(247,130,98,1) 100%);
      color: #fff;
    }
  }
  .my-button {
    display: flex;
    button {
      width: 50%;
      border: 0px;
      &:first-child {
        background-color: #ededed;
        color: #4F4F4F;
      }
      &:last-child {
        color: #fff;
        background:linear-gradient(90deg,rgba(249,97,84,1) 0%,rgba(247,130,98,1) 100%);
      }
    }
  }
  .my-list {
    box-sizing: border-box;
    padding: 0.3rem 0.3rem;
    border-bottom: 1px solid #f6f6f6;
    width: 100%;
    .my-list-row.van-row {
      margin: 0px !important;
      width: 100%;
      .my-img {
        width: 1.3rem;
      }
      .my-username {
        .my-one {
          font-size: 0.5rem;
          font-weight: 700;
          color: #5E5E5E;
        }
        .my-two {
          margin-left: 0.5rem;
          padding: 0.1rem 0.2rem;
          display: inline-block;
          background-color: #ffeae0;
          color: #FF7230;
          font-size: 0.35rem;
        }
      }
      .my-tip {
        font-size: 0.38rem;
        color: #A7AAB2;
      }
      .my-t {
        padding-top: 0.8rem;
        font-size: 0.35rem;
        color: #FA5151;
      }
    }
    .my-list-row2.van-row {
      margin: 0px !important;
      width: 100%;
      .my-one {
        padding-right: 0.05rem;
        border-right: 1px solid #f1f1f1;
        .my-ti {
          color: #FA5151;
          font-size: 0.55rem;
        }
        .my-ti2 {
          color:#A7AAB2;
          font-size: 0.4rem;
        }
      }
      .my-two {
        padding: 0.25rem 0 0 0.2rem;
        .my-ti {
          color: #596880;
          font-weight: 700;
          font-size: 0.4rem;
        }
        .my-ti2 {
          color:#A7AAB2;
          font-size: 0.4rem;
        }
      }
      .my-three {
        text-align: center;
        padding-top: 0.3rem;
        button.van-button--small {
          color: #fff;
          padding: 0 0.25rem;
          background:linear-gradient(90deg,rgba(249,97,84,1) 0%,rgba(247,130,98,1) 100%);
          box-shadow:0px 2px 7px 0px rgba(255,114,48,0.5);
        }
      }
    }
  }
  .my-scope {
    width: 100%;
    height: 50px;
  }
}
</style>
<style>
.van-field__left-icon {
  margin-right: 0px;
  left: 32%;
}
</style>