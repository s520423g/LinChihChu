<script>
import banner from "@/components/Banner.vue";
import artist from "@/components/Artist.vue";
import gluepainting from "@/components/Gluepainting.vue";
import work from "@/components/Work.vue";
import info from "@/components/Info.vue";
import statue from "@/components/Statue.vue";
import MenuTest from "@/components/Menu.vue";
import curator from "@/components/Curator.vue"; 
import background from "@/components/Background.vue";
import loading from "@/components/Loading.vue";




export default {
  components: {
    banner,
    statue,
    artist,
    MenuTest,
    gluepainting,
    work,
    info,
    curator,
    background,
    loading,
  },
  data() {
    return {
      showMenu: false, // 控制 menu 的顯示與隱藏
    };
  },
  mounted() {
    this.showMenuFunction();
  },

  methods: {
    showMenuFunction() {
      // 監聽 artist, gluepainting, work 區域的進入或離開
      const bannerSection = document.getElementById('banner');

      const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            this.showMenu = false;
            // console.log(this.showMenu);
          } else {
            this.showMenu = true;
          }
        });
      }, {
        threshold: 0.1, // 當至少 10% 區域進入視口時觸發
        rootMargin: '20px', // 可以調整觸發的提早或延遲
      });

      // 觀察每一個區域
      if (bannerSection) observer.observe(bannerSection);
      
    },
  },
};
</script>


<template>
    <loading />
    <statue />
    <div id="banner">
      <banner />
    </div>

    <div id="artist">
      <artist />
    </div>

    <div id="gluepainting">
      <div class="w-full h-[140px] flex flex-col justify-end pl-5 sm:pl-16 mb-[10px]">
            <div class="md:text-5xl text-3xl font-bold content-center">關於膠彩畫</div>
      </div>
      <gluepainting />
    </div>

    <div id="work">
      <div class="w-full h-[140px] flex flex-col justify-end pl-5 sm:pl-16 mb-[10px]">
            <div class="md:text-5xl text-3xl font-bold content-center">數位典藏</div>
      </div>
      <work />
    </div>
    <div id="curator">
      <div class="w-full h-[140px] flex flex-col justify-end pl-5 sm:pl-16">
            <div class="md:text-5xl text-3xl font-bold content-center">紀念館資訊</div>
      </div>
      <curator />
    </div>
  <MenuTest v-if="showMenu" />
  
  <footer>
    <div id="info">
      <info />
    </div>
  </footer>

<background />
</template>
