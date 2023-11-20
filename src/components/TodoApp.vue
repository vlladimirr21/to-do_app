<template>
  <div class="container">
    <h1 class="text-center mt-5">To-do list</h1>

    <!-- Поле ввода -->
    <div class="d-flex">
      <!-- директива для связки - связывает поле ввода с переменной -->
      <input
        v-model="item"
        type="text"
        placeholder="Enter item:"
        class="form-control"
      />
      <input
        v-model="title"
        type="text"
        placeholder="Enter title:"
        class="form-control"
      />

      <button @click="submitItems" class="btn btn-light rounded">
        <p>Create</p>
      </button>
    </div>

    <!-- Список элементов -->

    <table class="table table-bordered mt-5">
      <!-- Головка таблицы -->
      <thead>
        <tr class="text-center">
          <th scope="col">Name To-do</th>
          <th scope="col">Title</th>
          <th scope="col">Edit</th>
          <th scope="col">Delete</th>
        </tr>
      </thead>

      <!-- Прографка таблицы -->
      <tbody>
        <!-- v-for - директива для отображения  -->
        <tr v-for="(items, index) in items" :key="index">
          <th>{{ items.name }}</th>
          <td>{{ items.title }}</td>
          <td>
            <div class="text-center" @click="editItem(index)">
              <span class="fa fa-pen"></span>
            </div>
          </td>
          <td>
            <div class="text-center" @click="deleteItem(index)">
              <span class="fa fa-trash"></span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  // элементы массива
  data() {
    return {
      item: '',
      title: '',
      // для отслеживания индекса редактируемого элемента
      editedItem: null,
      items: [
        { name: 'First item', title: 'Title first to-do' },
        { name: 'Second item', title: 'Title second to-do' },
      ],
    }
  },

  methods: {
    // добавляет новый элемент в массив
    submitItems() {
      // если инпут пустой - ничего не добавлять
      if (this.item.length === 0) return

      if (this.editedItem === null) {
        this.items.push({
          name: this.item,
          title: this.title,
        })
      } else {
        this.items[this.editedItem].name = this.item
        this.editedItem = null
      }

      this.item = ''
      this.title = ''
    },
    // удаляет элемент из массива по переданному индексу
    deleteItem(index) {
      this.items.splice(index, 1)
    },
    // заполняет поля ввода для редактирования выбранной задачи
    editItem(index) {
      this.item = this.items[index].name
      this.editedItem = index
    },
  },
}
</script>
