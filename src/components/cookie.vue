<template>
    <div class="buttons">
      <button class="bg-gray-500 hover:bg-indigo-200 ..." @click="setCookie">Set Cookie</button>
      <button class="bg-green-500 hover:bg-indigo-200 ..." @click="getCookie">Get Cookie</button>
      <!-- <p >{{ cookieValue }}</p> -->
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        cookieValue: ''
      };
    },
    methods: {
      setCookie() {
        const cookieName = 'cookieName';
        const cookieValue = 'cookieValue';
        const expirationDays = 1;
  
        const date = new Date();
        date.setTime(date.getTime() + (expirationDays * 1 * 1 * 10 * 1000));
        const expires = "expires=" + date.toUTCString();
  
        document.cookie = cookieName + "=" + cookieValue + ";" + expires + ";path=/";
      },
      getCookie() {
        const cookieName = 'cookieName';
        const cookies = document.cookie.split(';');
  
        for (let i = 0; i < cookies.length; i++) {
          const cookie = cookies[i].trim();
          if (cookie.startsWith(cookieName + '=')) {
            this.cookieValue = cookie.substring(cookieName.length + 1);
            console.log(this.cookieValue)
            break;
          }
        }
      }
    }
  };
  </script>
  <style>
  button + button {
  margin-left: 35px;
  margin-bottom: 5px;
}
</style>


 
























