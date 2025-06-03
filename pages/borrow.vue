<template>
  <div class="p-6">
    <h1 class="text-3xl font-bold mb-6">我的借閱紀錄</h1>
    <table class="w-full border-collapse">
      <thead class="bg-gray-100">
        <tr>
          <th class="p-5 text-center border-2 border-gray-300 min-w-[400px] text-xl">書名</th>
          <th class="p-5 text-center border-2 border-gray-300 min-w-[200px] text-xl">作者</th>
          <th class="p-5 text-center border-2 border-gray-300 min-w-[150px] text-xl">借閱日期</th>
          <th class="p-5 text-center border-2 border-gray-300 min-w-[150px] text-xl">到期日</th>
          <th class="p-5 text-center border-2 border-gray-300 min-w-[120px] text-xl">操作</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(book, index) in books"
          :key="index"
          class="hover:bg-gray-50"
        >
          <td class="p-5 text-center border-2 border-gray-300 whitespace-normal break-words text-lg">{{ book.title }}</td>
          <td class="p-5 text-center border-2 border-gray-300 text-lg">{{ book.author }}</td>
          <td class="p-5 text-center border-2 border-gray-300 text-lg">{{ book.borrowDate }}</td>
          <td class="p-5 text-center border-2 border-gray-300 text-lg">{{ book.dueDate }}</td>
          <td class="p-5 text-center border-2 border-gray-300">
            <button
              class="bg-blue-500 text-white px-6 py-2 rounded hover:bg-blue-600 text-lg"
              @click="renewBook(index)"
            >
              續借
            </button>
          </td>
        </tr>
      </tbody>
    </table>

    <div v-if="message" class="mt-4 p-4 bg-green-100 text-green-800 rounded-lg text-lg">
      {{ message }}
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const books = ref([])
const message = ref('')

const fetchBooks = async () => {
  // 模擬資料
  books.value = [
    {
      title: 'Harry Potter and the Philosopher\'s Stone',
      author: 'J. K. Rowling',
      borrowDate: '2025-05-31',
      dueDate: '2025-07-03'
    },
    {
      title: 'Harry Potter and the Order of the Phoenix',
      author: 'J. K. Rowling',
      borrowDate: '2025-05-28',
      dueDate: '2025-07-03'
    },
    {
      title: 'Harry Potter and the Deathly Hallows',
      author: 'J. K. Rowling',
      borrowDate: '2025-05-25',
      dueDate: '2025-07-03'
    },
    {
      title: 'Harry Potter and the Prisoner of Azkaban',
      author: 'J. K. Rowling',
      borrowDate: '2025-05-22',
      dueDate: '2025-07-03'
    },
    {
      title: 'Harry Potter and the Chamber of Secrets',
      author: 'J. K. Rowling',
      borrowDate: '2025-05-19',
      dueDate: '2025-07-03'
    },
    {
      title: 'Harry Potter and the Half-Blood Prince',
      author: 'J. K. Rowling',
      borrowDate: '2025-05-16',
      dueDate: '2025-07-03'
    },
    {
      title: 'Harry Potter and the Goblet of Fire',
      author: 'J. K. Rowling',
      borrowDate: '2025-05-13',
      dueDate: '2025-07-03'
    },
    {
      title: 'Harry Potter',
      author: 'Warner Bros. Entertainment Inc',
      borrowDate: '2025-05-10',
      dueDate: '2025-07-03'
    },
    {
      title: 'Harry Potter',
      author: 'J. K. Rowling',
      borrowDate: '2025-05-07',
      dueDate: '2025-07-03'
    },
    {
      title: 'Harry Potter (series) 1-7',
      author: 'J. K. Rowling',
      borrowDate: '2025-05-04',
      dueDate: '2025-07-03'
    }
  ]
}

const renewBook = (index) => {
  const newDueDate = new Date()
  newDueDate.setDate(newDueDate.getDate() + 30)
  books.value[index].dueDate = newDueDate.toISOString().split('T')[0]
  message.value = `《${books.value[index].title}》續借成功！新的到期日為 ${books.value[index].dueDate}`

  setTimeout(() => (message.value = ''), 3000)
}

onMounted(fetchBooks)
</script>

<style scoped>
.material-icons {
  font-family: 'Material Icons';
  font-weight: normal;
  font-style: normal;
  font-size: 24px;
  line-height: 1;
  letter-spacing: normal;
  text-transform: none;
  display: inline-block;
  white-space: nowrap;
  word-wrap: normal;
  direction: ltr;
  -webkit-font-smoothing: antialiased;
}
</style>
