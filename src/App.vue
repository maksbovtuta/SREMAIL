<template>
  <div class="bg-gray-100 min-h-screen flex items-center justify-center">
    <div class="bg-white w-full max-w-md p-6 rounded-lg shadow-md">
      <h1 class="text-3xl font-semibold mb-6 text-center text-blue-600">Форма для надсилання повідомлення про корупцію</h1>
      <form>
        <div class="mb-6">
          <label for="name" class="block text-gray-600 text-sm font-medium mb-2">Прізвище, ім'я, по батькові особи, яка вчинила правопорушення:</label>
          <input type="text" id="name" v-model="name" required class="w-full border rounded-md py-2 px-3 focus:outline-none focus:ring focus:border-blue-300">
        </div>

        <div class="mb-6">
          <label for="position" class="block text-gray-600 text-sm font-medium mb-2">Посада особи:</label>
          <input type="text" id="position" v-model="position" required class="w-full border rounded-md py-2 px-3 focus:outline-none focus:ring focus:border-blue-300">
        </div>

        <div class="mb-6">
          <label for="workplace" class="block text-gray-600 text-sm font-medium mb-2">Місце роботи:</label>
          <input type="text" id="workplace" v-model="workplace" required class="w-full border rounded-md py-2 px-3 focus:outline-none focus:ring focus:border-blue-300">
        </div>

        <div class="mb-6">
          <label for="message" class="block text-gray-600 text-sm font-medium mb-2">Текст повідомлення:</label>
          <textarea id="message" v-model="message" required class="w-full border rounded-md py-2 px-3 focus:outline-none focus:ring focus:border-blue-300"></textarea>
        </div>

        <div class="mb-6">
          <label class="block text-gray-600 text-sm font-medium mb-2">Анонимная отправка</label>
          <input type="checkbox" v-model="anonymous" class="form-checkbox h-5 w-5 text-blue-600">
        </div>
        
        <div class="mb-6">
          <label class="block text-gray-600 text-sm font-medium mb-2" v-if="!anonymous">Автор повідомлення:</label>
          <input type="text" id="author" v-model="author" class="w-full border rounded-md py-2 px-3 focus:outline-none focus:ring focus:border-blue-300" v-if="!anonymous">
        </div>

        

        <div class="mt-6">
          <button @click = "submitForm()" type="button" class="w-full bg-blue-500 text-white rounded-md py-2 px-4 hover:bg-blue-600 focus:outline-none focus:ring focus:border-blue-300">
            Відправити повідомлення
          </button>
        </div>
      </form>
    </div>
  </div>
</template>


<script>
import emailjs from 'emailjs-com';

export default {
  data() {
    return {
      name: '',
      position: '',
      workplace: '',
      message: '',
      author: '',
      anonymous: false

    };
  },
  methods: {
    submitForm() {
      emailjs.send("service_vfkd7m4", "template_mppapc1", {
        'name': this.name,
        // 'position': this.position,
        // 'workplace': this.workplace,
        'message': this.position + ' ' + this.workplace + ' ' + this.message,
        'author': this.author
      }, "OSvMpS4wtzweRF6o7")
        .then(response => {
          console.log('Повідомлення успішно відправлене:', response);
        })
        .catch(error => {
          console.error('Помилка відправки повідомлення:', error);
        });
    }
  }
};
</script>


