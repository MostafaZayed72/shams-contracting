<template>
    <div>
        <Loader v-if="loader" />
      <!-- زر إضافة قسم جديد -->
      <Button label="إضافة قسم جديد" icon="pi pi-plus" @click="showDialog = true" class="mb-4 bg-primary"/>
  
      <!-- نافذة حوار لإضافة قسم جديد -->
      <Dialog header="إضافة قسم جديد" :visible="showDialog" @hide="resetForm" :modal="true" :closable="false" :style="$i18n.locale === 'ar-AR' ? 'direction: rtl' : ''">
        <!-- زر إغلاق في أعلى النافذة -->
        <template #header>
          <div class="flex justify-between items-center">
            <span>إضافة قسم جديد</span>
            <Button icon="pi pi-times" class="p-button-rounded p-button-text" @click="closeDialog" />
          </div>
        </template>
  
        <form @submit.prevent="addDepartment">
          <div class="p-fluid">
            <div class="field">
              <label for="title">العنوان</label>
              <InputText id="title" v-model="department.title" placeholder="أدخل العنوان" class="w-full"/>
            </div>
  
            <div class="field">
              <label for="description">الوصف</label>
              <InputText id="description" v-model="department.description" placeholder="أدخل الوصف" rows="3" class="w-full"/>
            </div>
  
            <div class="field">
              <label for="imageUrl">رابط الصورة</label>
              <InputText id="imageUrl" v-model="department.imageUrl" placeholder="أدخل رابط الصورة" class="w-full"/>
            </div>
  
            <!-- <div class="field">
              <label for="icon">الأيقونة</label>
              <InputText id="icon" v-model="department.icon" placeholder="أدخل الأيقونة" class="w-full"/>
            </div> -->
  
            <div class="field mt-4 flex justify-center gap-4">
                <Button label="إغلاق" class=" bg-red-darken-4 w-1/2" @click="closeDialog" />

              <Button label="إضافة"  type="submit" class="w-1/2"/>

            </div>
          </div>
        </form>
      </Dialog>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  import  Dialog  from 'primevue/dialog'
  import  Button  from 'primevue/button'
  import  InputText  from 'primevue/inputtext'
  import axios from 'axios'
  
  const loader = ref() 
  // الوصول إلى base URL من .env
  const baseUrl = import.meta.env.VITE_API_BASE_URL
  
  // حالة نافذة الحوار
  const showDialog = ref(false)
  
  // نموذج البيانات لإضافة قسم
  const department = ref({
    title: '',
    description: '',
    imageUrl: '',
    icon: ''
  })
  
  // دالة لإرسال البيانات إلى الـ API
  const addDepartment = async () => {
    loader.value=true
    try {
      const response = await axios.post(`${baseUrl}/api/Departments/AddDepartment`, department.value)
      console.log('القسم تم إضافته بنجاح', response.data)
      showDialog.value = false
      resetForm()
      loader.value=false
    } catch (error) {
      console.error('خطأ أثناء إضافة القسم', error)
    }
  }
  
  // دالة لإعادة تعيين النموذج بعد الإرسال أو إغلاق الحوار
  const resetForm = () => {
    department.value = {
      title: '',
      description: '',
      imageUrl: ''
      
    }
  }
  
  // دالة لإغلاق نافذة الحوار
  const closeDialog = () => {
    showDialog.value = false
    resetForm()
  }
  </script>
  
  <style scoped>
  /* تخصيص الأنماط هنا إذا لزم الأمر */
  </style>
  