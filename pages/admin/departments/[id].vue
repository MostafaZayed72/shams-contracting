<template>
  <div class="p-4 ">
    <Loader v-if="loader" />
    <h2 class="text-xl mb-4">تعديل القسم</h2>

    <!-- نموذج التعديل -->
    <form @submit.prevent="updateDepartment">
      <div class="field">
        <label for="title">العنوان</label>
        <InputText id="title" v-model="department.title" placeholder="أدخل العنوان" class="w-full" />
      </div>

      <div class="field mt-3">
        <label for="description">الوصف</label>
        <InputTextarea id="description" v-model="department.description" placeholder="أدخل الوصف" rows="3" class="w-full" />
      </div>

      <div class="field mt-3">
        <label for="imageUrl">رابط الصورة</label>
        <InputText id="imageUrl" v-model="department.imageUrl" placeholder="أدخل رابط الصورة" class="w-full" />
      </div>

      <div class="field mt-4 flex justify-between">
        <Button label="تعديل" icon="pi pi-check" type="submit" class="w-1/3" />
        <Button label="حذف القسم" icon="pi pi-trash" @click="deleteDepartment" class="w-1/3 p-button-danger" />
      </div>
    </form>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import InputText from 'primevue/inputtext'
import Button from 'primevue/button'
import axios from 'axios'

// الحصول على route
const route = useRoute()
const router = useRouter()
const loader= ref()
// الوصول إلى base URL من .env
const baseUrl = import.meta.env.VITE_API_BASE_URL

// تعريف البيانات
const department = ref({
  id: 0,
  title: '',
  description: '',
  imageUrl: ''
})

// دالة لجلب بيانات القسم عند تحميل المكون
const getDepartmentById = async () => {
  loader.value= true
  const id = route.params.id
  try {
    const response = await axios.get(`${baseUrl}/api/Departments/GetDepartmentById`, {
      params: { id }
    })
    department.value = response.data
 loader.value = false } catch (error) {
    console.error('خطأ أثناء جلب بيانات القسم', error)
  }
}

// دالة لتعديل القسم
const updateDepartment = async () => {
  loader.value= true
  try {
    const response = await axios.put(`${baseUrl}/api/Departments/UpdateDepartment`, department.value)
    console.log('تم تعديل القسم بنجاح', response.data)
    router.push('/admin/departments') // التوجيه إلى صفحة الأقسام
 loader.value = false } catch (error) {
    console.error('خطأ أثناء تعديل القسم', error)
  }
}

// دالة لحذف القسم
const deleteDepartment = async () => {
  loader.value= true
  const confirmed = confirm('هل أنت متأكد أنك تريد حذف هذا القسم؟')
  if (confirmed) {
    try {
      const id = department.value.id
      const response = await axios.delete(`${baseUrl}/api/Departments/DeleteDepartment`, {
        params: { id }
      })
      console.log('تم حذف القسم بنجاح', response.data)
      router.push('/admin/departments') // التوجيه إلى صفحة الأقسام بعد الحذف
   loader.value = false } catch (error) {
      console.error('خطأ أثناء حذف القسم', error)
    }
  }
}

// تنفيذ دالة جلب بيانات القسم عند تحميل المكون
onMounted(() => {
  getDepartmentById()
})
definePageMeta({
  layout: "admin"
});

</script>

<style scoped>
/* تخصيص الأنماط هنا إذا لزم الأمر */
</style>
