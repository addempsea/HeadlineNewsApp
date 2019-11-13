<template>
  <div class="container-fluid">
    <h1 class="mb-3">Top Headlines from around the world</h1>
    <form class="container">
      <div class="input-group mb-3">
        <div class="input-group-prepend">
          <label class="input-group-text" for="inputGroupSelect01">Country</label>
        </div>
        <select class="custom-select" id="inputGroupSelect01" v-model="country">
          <option value="us">USA</option>
          <option value="ng">Nigeria</option>
          <option value="de">Germany</option>
          <option value="jp">Japan</option>
          <option value="nz">New Zealand</option>
          <option value="gb">England</option>
          <option value="ca">Canada</option>
        </select>
      </div>

      <div class="input-group mb-3">
        <div class="input-group-prepend">
          <label class="input-group-text" for="inputGroupSelect01">Category</label>
        </div>
        <select class="custom-select" id="inputGroupSelect01" v-model="category">
          <option value="general">General</option>
          <option value="health">Health</option>
          <option value="science">Science</option>
          <option value="sports">Sports</option>
          <option value="entertainment">Entertainment</option>
          <option value="technology">Tech</option>
          <option value="business">Business</option>
        </select>
      </div>
      <button type="button" class="btn btn-dark mb-3" @click="getNews">Get News</button>
    </form>
    <!-- <div class="media">
        <img class="mr-3 images" :src="item.urlToImage" :alt="item.title" />
        <div class="media-body">
            <a :href="item.url" ><h5 class="mt-0">{{item.title}}</h5></a> 
            {{item.description}}
        </div>
    </div> -->

    <div>
        <div class="main__hero" v-for="(item, index) in items" :key="index">
            <a :href="item.url" class="picture__link" target="_blank">
                <div>
                    <img :src="item.urlToImage" :alt="item.title" class="images">
                </div>
            </a>
            <div class="content__body">
                <!-- <ul class="source__holder">
                    <li>
                        <a :href="item.source.name + '.com'">
                            <span>
                                {{item.source.name}}
                            </span>
                        </a>
                    </li>
                </ul> -->
                <h2>
                    <a :href="item.url" target="_blank">
                        {{item.title}}
                    </a>
                </h2>
                <p>
                    {{item.description}}
                </p>
                
                <div>
                    <span class="time">{{item.publishedAt}}</span> 
                    <span></span>
                </div>
                <hr> <hr>
            </div>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Api",
  data() {
    return {
      country: "",
      category: "",
      items: []
    };
  },

  methods: {
    getNews() {
      var apiSource = "https://newsapi.org/v2/top-headlines?country=";
      var ctr = this.country;
      var linkup = "&category=";
      var cat = this.category;
      var apiKey = "&apiKey=360e9255e3ce425881637a308ecf0632";
      var source = apiSource + ctr + linkup + cat + apiKey;
      this.$http.get(source).then(response => {
        this.items = response.data.articles;
      });
    }
  }
};
</script>
<style scoped>
    .main__hero {
        align-items: flex-start;
        display: flex;
        width: 100%;
        margin-bottom: 30px;
    }

    .picture__link {
        position: relative;
        width: 30%;
        height: 100%;
    }

    .images {
        display: block;
        height: 120px;
        margin: 0;
        padding: 0;
        position: absolute;
        top: 0;
        width: 320px;
        z-index: 21;
        background-position: 50%;
        background-size: cover;
        object-fit: cover;
    }

    .content__body {
        flex-grow: 1;
        padding: 0 8px;
        width: 70%;
    }

    .time {
      color: tomato;
    }

@media screen and (max-width: 480px) {
  .images{
    display: none;
  }
}


</style>
