<template>
  <div class="cart">
    <!-- 时间选择器 -->
    <van-field
      v-model="state.pickerValue"
      readonly
      clickable
      name="datetimePicker"
      label="时间选择"
      placeholder="点击选择时间"
      @click="state.showPicker = true"
    />
    <van-popup v-model:show="state.showPicker" position="bottom">
      <van-datetime-picker
        type="time"
        @confirm="onPickerConfirm"
        @cancel="state.showPicker = false"
      />
    </van-popup>
    <!-- 省市区选择器 -->
    <van-field
      v-model="state.areaValue"
      readonly
      clickable
      name="area"
      label="地区选择"
      placeholder="点击选择省市区"
      @click="state.showArea = true"
    />
    <van-popup v-model:show="state.showArea" position="bottom">
      <van-area
        :area-list="areaList"
        @confirm="onAreaConfirm"
        @cancel="state.showArea = false"
      />
    </van-popup>
  </div>
  <Docker :currentIndex="1" />
</template>

<script>
import Docker from '../../components/Docker';
import { areaList } from '@vant/area-data';
import { reactive } from 'vue';
export default {
  name: 'CartList',
  components: { Docker },
  setup() {
    const state = reactive({
      pickerValue: '',
      areaValue: '',
      showPicker: false,
      showArea: false
    });
    const onPickerConfirm = value => {
      state.pickerValue = value;
      state.showPicker = false;
    };
    const onAreaConfirm = value => {
      state.areaValue =
        value[0].name + '/' + value[1].name + '/' + value[2].name;
      state.showArea = false;
    };
    return {
      state,
      areaList,
      onPickerConfirm,
      onAreaConfirm
    };
  }
};
</script>

<style lang="scss" scoped>
.cart {
  margin-top: 0.2rem;
  text-align: center;
}
</style>
