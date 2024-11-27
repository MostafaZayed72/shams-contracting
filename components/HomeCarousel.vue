<template>
  <div>
    <v-carousel :height="carouselHeight" show-arrows="false" cycle hide-delimiter-background>
      <v-carousel-item>
        <div class="relative">
          <img class="sm:w-100 md:w-[70%] px-4 rounded-xl relative cursor-pointer h-48 md:h-[400px] mx-auto"
            src="https://www.economy-today.com/economy/uploads/2021/09/%D8%A8%D8%B1%D8%AC-%D8%A7%D9%84%D9%85%D9%85%D9%84%D9%83%D8%A9-750x430.jpg" alt="Image" @click="navigateTo('/article')" />

        </div>
      </v-carousel-item>
     
      <v-carousel-item>
        <div class="relative">
          <img class="sm:w-100 md:w-[70%] px-4 rounded-xl relative cursor-pointer h-48 md:h-[400px] mx-auto"
            src="https://argaamplus.s3.amazonaws.com/961f0e5d-670c-4b01-8f2a-a5c0134fca43.png" alt="Image" @click="navigateTo('/article')" />

        </div>
      </v-carousel-item>
      <v-carousel-item>
        <div class="relative">
          <img class="sm:w-100 md:w-[70%] px-4 rounded-xl relative cursor-pointer h-48  md:h-[400px] mx-auto"
            src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/20/Riyadh_Skyline.jpg/1200px-Riyadh_Skyline.jpg" alt="Image" @click="navigateTo('/article')" />

        </div>
      </v-carousel-item>
      <v-carousel-item>
        <div class="relative">
          <img class="sm:w-100 md:w-[70%] px-4 rounded-xl relative cursor-pointer h-48  md:h-[400px] mx-auto"
            src="https://m.eyeofriyadh.com/news_images/2018/03/1b41e0e013581.jpg" alt="Image" @click="navigateTo('/article')" />

        </div>
      </v-carousel-item>
     

    

    </v-carousel>
  </div>
</template>


<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const carouselHeight = ref(250); // الطول الافتراضي للشاشات الصغيرة
const products = ref([]); // لتخزين المنتجات

// دالة لتحديث الارتفاع بناءً على حجم الشاشة
const updateHeight = () => {
  if (window.innerWidth >= 580) {
    carouselHeight.value = 450; // الطول للشاشات الكبيرة جدًا
  } else if (window.innerWidth >= 490) {
    carouselHeight.value = 350; // الطول للشاشات الكبيرة
  } else if (window.innerWidth >= 410) {
    carouselHeight.value = 300; // الطول للشاشات المتوسطة
  } else {
    carouselHeight.value = 240; // الطول للشاشات الصغيرة
  }
};

// دالة لجلب المنتجات
const fetchProducts = async () => {
  try {
    const response = await fetch(`${import.meta.env.VITE_API_BASE_URL}/api/Products/GetAllProducts`);
    const data = await response.json();
    products.value = data.data.map(product => ({
      id: product.id,
      imageUrl: `${import.meta.env.VITE_API_BASE_URL}/${product.images?.[0]?.url}`, // استخدام أول صورة مع المسار الكامل
    }));

  } catch (error) {
    console.error("Error fetching products:", error);
  }
};

onMounted(() => {
  updateHeight(); // تعيين الارتفاع عند تحميل الصفحة
  fetchProducts(); // جلب المنتجات عند تحميل الصفحة

  // إضافة مستمع للحدث resize لتحديث الارتفاع عند تغيير حجم الشاشة
  window.addEventListener('resize', updateHeight);
});

onUnmounted(() => {
  // إزالة مستمع الحدث عند التخلص من المكون
  window.removeEventListener('resize', updateHeight);
});
</script>




<style>
.v-btn--icon.v-btn--density-default {
  background-color: rgb(3, 102, 56) !important;
  height: 12px !important;
  width: 12px !important;
}

.v-btn--icon.v-btn--density-default {
  color: rgb(251, 250, 252) !important;

}

.mdi:before {
  display: none !important
}

.v-window__right {
  display: none !important
}

.v-window__left {
  display: none !important
}
</style>
