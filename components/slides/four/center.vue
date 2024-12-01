<template>
    <div>
        <h1 class="text-white text-center text-3xl font-bold">{{ $t('Our Departments') }}</h1>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6 p-8">
      <!-- المربع الأول -->
      <div v-for="(section, index) in sections" 
           :key="index" 
           class="relative group rounded-lg overflow-hidden shadow-lg cursor-pointer">
        <img :src="section.image" alt="section.name" class="w-full h-48 object-cover">
        <div class="absolute inset-0 bg-gray-900 bg-opacity-0 group-hover:bg-opacity-80 transition duration-300 flex items-center justify-center delayed">
          <p class="text-gray-300 text-lg opacity-0 group-hover:opacity-100 transition duration-300 text-center px-4 delayed">
            {{ section.description }}
          </p>
        </div>
        <div class="p-4 text-center bg-primary">
          <h3 class="text-lg font-semibold">{{ section.name }}</h3>
        </div>
      </div>
    </div>
    </div>
  </template>
  
  <script setup>
  const sections = [
    { name: 'الهندسة', image: 'https://img.freepik.com/free-vector/laptop-with-program-code-isometric-icon-software-development-programming-applications-dark-neon_39422-971.jpg', description: 'قسم الهندسة يوفر حلولاً متقدمة' },
    { name: 'التدريب', image: 'https://it5.alhuda.com.pk/wp-content/uploads/2023/10/k3.png', description: 'التدريب لتعزيز المهارات' },
    { name: 'بناء', image: 'https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgt0A_brt0Z-XdOYkcBvO3JfDsyt6BfU86ITOwjIyuax-vyxb6veZzDo_ZNIe7k1_EzozouktiCoSH0PSEEcKYcXQRbT6UypsRar_Tro-M6HBFnh9YYxVI2uIjVMufujpVgGPTPuJ_Jz9M1/s1600/1408241940103919-net_software_programmer.jpg', description: 'خدمات بناء متميزة' },
    { name: 'التطوير', image: 'https://trend.m7et.com/wp-content/uploads/2022/10/%D8%A8%D8%AD%D8%AB-%D8%B9%D9%86-%D9%84%D8%BA%D8%A7%D8%AA-%D8%A7%D9%84%D8%A8%D8%B1%D9%85%D8%AC%D8%A9-1024x683.jpg', description: 'حلول التطوير الشاملة' },
    { name: 'التمويل', image: 'https://png.pngtree.com/thumb_back/fh260/background/20231004/pngtree-3d-illustration-of-web-development-programming-code-on-laptop-screen-image_13531204.png', description: 'خدمات تمويل متكاملة' }
  ];
  </script>
  
  <style scoped>
  .group:hover .group-hover\:bg-opacity-80 {
    background-color: rgba(0, 0, 0, 0.8);
  }
  
  /* تأكد من أن النص يظهر عند الـ hover */
  .group:hover .group-hover\:opacity-100 {
    opacity: 1 !important;
  }
  </style>
  