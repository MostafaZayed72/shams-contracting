<template>
    <div>
      <DataTable :value="departments" paginator rows="10" :totalRecords="totalCount" class="p-datatable-responsive">
        <Column class="text-center" field="title" header="العنوان" />
        <Column class="text-center" field="description" header="الوصف" />
        <!-- عمود صورة -->
        <Column class="text-center mx-auto" header="رابط الصورة">
          <template #body="{ data }">
            <img v-if="data.imageUrl" :src="data.imageUrl" alt="Image" class="w-20 h-20 rounded-xl object-cover mx-auto" />
            <span v-else>لا توجد صورة</span>
          </template>
        </Column>
        <!-- عمود زر التعديل -->
        <Column header="الإجراء" class="text-center">
          <template #body="{ data }">
            <Button 
              label="تعديل" 
              icon="pi pi-pencil" 
              class="bg-yellow"
              @click="editDepartment(data.id)" />
          </template>
        </Column>
      </DataTable>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue'
  import { useRouter } from 'vue-router' // لاستخدام التوجيه
  import DataTable from 'primevue/datatable'
  import Column from 'primevue/column'
  import Button from 'primevue/button'
  import axios from 'axios'
  
  // الوصول إلى base URL من .env
  const baseUrl = import.meta.env.VITE_API_BASE_URL
  
  // تعريف البيانات
  const departments = ref([])
  const totalCount = ref(0)
  
  // الحصول على الدالة الخاصة بالتوجيه
  const router = useRouter()
  
  // دالة لجلب الأقسام من الـ API
  const getDepartments = async () => {
    try {
      const response = await axios.get(`${baseUrl}/api/Departments/GetDepartments`)
      departments.value = response.data.data
      totalCount.value = response.data.totalCount
    } catch (error) {
      console.error('خطأ أثناء جلب الأقسام', error)
    }
  }
  
  // تنفيذ الدالة عند تحميل المكون
  onMounted(() => {
    getDepartments()
  })
  
  // دالة لتحويل المستخدم إلى صفحة التعديل
  const editDepartment = (id) => {
    router.push(`/admin/departments/${id}`)
  }
  </script>
  
  <style scoped>
  /* تخصيص الأنماط هنا إذا لزم الأمر */
  </style>
  