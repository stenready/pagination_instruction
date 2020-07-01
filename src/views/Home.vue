<template>
  <div class="home">
    <el-main>
      <el-row type="flex"  :gutter="20" style="flex-wrap: wrap" v-if="current_el">
        <el-col
          :sm="24"
          :lg="6"
          :md="12"
          v-for="(el) of current_el"
          :key="el.id"
          class="flex_col"
          style="margin-bottom: 1rem;"
        >
          <el-card>
            <p class="home_title">{{el.title}}</p>
            <p>{{el.body}}</p>
          </el-card>
        </el-col>
      </el-row>
      <div class="flex_wrapper_my">
        <el-pagination
          prev-text="Назад"
          next-text="Вперёд"
          :page-size="+elems_on_page"
          background
          layout="prev, pager, next"
          :total="elements.length"
          @current-change="mySuperChange"
          :current-page="page"
        ></el-pagination>
        <el-select v-model="elems_on_page" @change="changePaginationLength" placeholder="Select">
          <el-option label="по 5 елементов" value="5"></el-option>
          <el-option label="по 10 елементов" value="10"></el-option>
          <el-option label="по 20 елементов" value="20"></el-option>
          <el-option label="по 50 елементов" value="50"></el-option>
          <el-option label="по 100 елементов" value="100"></el-option>
        </el-select>
      </div>
    </el-main>
  </div>
</template>

<script>
import axios from "axios";
import _ from "lodash";
export default {
  name: "Home",

  methods: {
    mySuperChange(el) { //изменение при пагинации
      this.$router.push(`${this.$route.path}?page=${el}`);
      this.current_el =
        this.current_elements[el - 1] || this.current_elements[0];
    },
    changePaginationLength(el) { //выбор селект длинны пагинации (изменение)
      this.current_elements = _.chunk(this.elements, +el);
      this.current_el =
        this.current_elements[this.page - 1] || this.current_elements[0];
    }
  },
  data() {
    return {
      elements: [],  //все загруженные елементы
      page: +this.$route.query.page || 1,
      current_elements: [],
      current_el: null, // текущий массив страницы
      elems_on_page: "5", //количество елементов на одной странице
      selected_data: null
    };
  },
  components: {},
  mounted() {
    axios("https://jsonplaceholder.typicode.com/posts").then(res => {
      this.elements = res.data;
      this.current_elements = _.chunk(res.data, this.elems_on_page);
      this.current_el =
        this.current_elements[this.page - 1] || this.current_elements[0];
    });
  }
};
</script>

<style lang="scss">
.home_title {
  font-size: 1.2rem;
  font-weight: 600;
}
.el-card {
  height: 100%;
}
.flex_wrapper_my {
  display: flex;
  align-items: center;
}
.el-input__inner{
  width: 175px !important;
}
</style>
