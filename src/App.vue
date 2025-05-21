<script setup>
import { ref, onMounted } from 'vue';
import LoginPopup from './components/LoginPopup.vue';

// With script setup, use ref instead of data() method
const showLoginPopup = ref(false);
const isLoggedIn = ref(false);
const user = ref(null);

// Check if user is logged in on component mount
onMounted(() => {
  checkAuthStatus();
});

// Function to check authentication status
const checkAuthStatus = () => {
  const token = localStorage.getItem('token');
  const userData = localStorage.getItem('user');
  if (token && userData) {
    user.value = JSON.parse(userData);
    isLoggedIn.value = true;
  }
};

// Function to handle logout
const handleLogout = () => {
  localStorage.removeItem('token');
  localStorage.removeItem('user');
  isLoggedIn.value = false;
  user.value = null;
};

// Function called when login is successful
const onLoginSuccess = (userData, token) => {
  localStorage.setItem('token', token);
  localStorage.setItem('user', JSON.stringify(userData));
  user.value = userData;
  isLoggedIn.value = true;
  showLoginPopup.value = false;
};
</script>
<template>
  <div>
    <div class="desktop-nav hidden md:block">
      <nav class="flex justify-between items-center px-8 md:px-12 lg:px-32 xl:px-48 py-4 bg-gray-400">
        <div class="navbar-utility flex gap-2">
          <a href="/">
            <img
              src="https://imgs.search.brave.com/5z3y1_Y3lst6b4j7yo9x-jS0MJ5yQZmmLUHNDcCDdkU/rs:fit:860:0:0:0/g:ce/aHR0cHM6Ly9tZWRp/YS5pc3RvY2twaG90/by5jb20vaWQvMTM0/NDMyMzUyOC9waG90/by9zaG90LW9mLWEt/eW91bmctYnVzaW5l/c3NtYW4td29ya2lu/Zy1vbi1hLWNvbXB1/dGVyLWluLWFuLW9m/ZmljZS5qcGc_cz02/MTJ4NjEyJnc9MCZr/PTIwJmM9NjJJX3B4/ZExfZ3VQZmpXSzA1/VXlKbzIxWVNNQ29f/aDB5bnNjNm5IWmgz/bz0"
              alt="" class="w-10 h-10 object-cover rounded-full" />
          </a>
          <button class="flex justify-center items-center gap-2 bg-gray-200 px-4 py-2 rounded-full font-semibold">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
              stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
              class="icon icon-tabler icons-tabler-outline icon-tabler-search">
              <path stroke="none" d="M0 0h24v24H0z" fill="none" />
              <path d="M10 10m-7 0a7 7 0 1 0 14 0a7 7 0 1 0 -14 0" />
              <path d="M21 21l-6 -6" />
            </svg>
            <span>Search</span>
          </button>
          <div class="bg-gray-200 flex justify-center items-center gap-3 px-4 py-2 rounded-full font-semibold">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
              stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
              class="icon icon-tabler icons-tabler-outline icon-tabler-calendar-plus">
              <path stroke="none" d="M0 0h24v24H0z" fill="none" />
              <path d="M12.5 21h-6.5a2 2 0 0 1 -2 -2v-12a2 2 0 0 1 2 -2h12a2 2 0 0 1 2 2v5" />
              <path d="M16 3v4" />
              <path d="M8 3v4" />
              <path d="M4 11h16" />
              <path d="M16 19h6" />
              <path d="M19 16v6" />
            </svg>
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="currentColor"
              class="icon icon-tabler icons-tabler-filled icon-tabler-layout">
              <path stroke="none" d="M0 0h24v24H0z" fill="none" />
              <path d="M8 3a3 3 0 0 1 3 3v1a3 3 0 0 1 -3 3h-2a3 3 0 0 1 -3 -3v-1a3 3 0 0 1 3 -3z" />
              <path d="M8 12a3 3 0 0 1 3 3v3a3 3 0 0 1 -3 3h-2a3 3 0 0 1 -3 -3v-3a3 3 0 0 1 3 -3z" />
              <path d="M18 3a3 3 0 0 1 3 3v12a3 3 0 0 1 -3 3h-2a3 3 0 0 1 -3 -3v-12a3 3 0 0 1 3 -3z" />
            </svg>
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
              stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
              class="icon icon-tabler icons-tabler-outline icon-tabler-books">
              <path stroke="none" d="M0 0h24v24H0z" fill="none" />
              <path d="M5 4m0 1a1 1 0 0 1 1 -1h2a1 1 0 0 1 1 1v14a1 1 0 0 1 -1 1h-2a1 1 0 0 1 -1 -1z" />
              <path d="M9 4m0 1a1 1 0 0 1 1 -1h2a1 1 0 0 1 1 1v14a1 1 0 0 1 -1 1h-2a1 1 0 0 1 -1 -1z" />
              <path d="M5 8h4" />
              <path d="M9 16h4" />
              <path
                d="M13.803 4.56l2.184 -.53c.562 -.135 1.133 .19 1.282 .732l3.695 13.418a1.02 1.02 0 0 1 -.634 1.219l-.133 .041l-2.184 .53c-.562 .135 -1.133 -.19 -1.282 -.732l-3.695 -13.418a1.02 1.02 0 0 1 .634 -1.219l.133 -.041z" />
              <path d="M14 9l4 -1" />
              <path d="M16 16l3.923 -.98" />
            </svg>
          </div>
        </div>
        <div class="navbar-button">
          <!-- Conditional rendering based on auth state -->
          <button v-if="!isLoggedIn"
            class="flex justify-center items-center gap-2 bg-gray-200 px-4 py-2 rounded-full font-semibold"
            @click="showLoginPopup = true">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
              stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
              class="icon icon-tabler icons-tabler-outline icon-tabler-login-2">
              <path stroke="none" d="M0 0h24v24H0z" fill="none" />
              <path d="M9 8v-2a2 2 0 0 1 2 -2h7a2 2 0 0 1 2 2v12a2 2 0 0 1 -2 2h-7a2 2 0 0 1 -2 -2v-2" />
              <path d="M3 12h13l-3 -3" />
              <path d="M13 15l3 -3" />
            </svg>
            <span>Sign In</span>
          </button>

          <!-- User profile when logged in -->
          <div v-else class="flex items-center gap-2">
            <div class="text-sm font-medium">{{ user?.email }}</div>
            <button class="flex justify-center items-center gap-2 bg-gray-200 px-4 py-2 rounded-full font-semibold"
              @click="handleLogout">
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                <path d="M14 8v-2a2 2 0 0 0 -2 -2h-7a2 2 0 0 0 -2 2v12a2 2 0 0 0 2 2h7a2 2 0 0 0 2 -2v-2" />
                <path d="M7 12h14l-3 -3m0 6l3 -3" />
              </svg>
              <span>Logout</span>
            </button>
          </div>
        </div>
      </nav>
    </div>
    <div class="mobile-nav block md:hidden">
      <nav class="flex justify-between items-center gap-2 px-8 md:px-12 lg:px-32 xl:px-48 py-4 bg-gray-400">
        <div class="navbar-utility flex gap-2 w-100">
          <img
            src="https://imgs.search.brave.com/5z3y1_Y3lst6b4j7yo9x-jS0MJ5yQZmmLUHNDcCDdkU/rs:fit:860:0:0:0/g:ce/aHR0cHM6Ly9tZWRp/YS5pc3RvY2twaG90/by5jb20vaWQvMTM0/NDMyMzUyOC9waG90/by9zaG90LW9mLWEt/eW91bmctYnVzaW5l/c3NtYW4td29ya2lu/Zy1vbi1hLWNvbXB1/dGVyLWluLWFuLW9m/ZmljZS5qcGc_cz02/MTJ4NjEyJnc9MCZr/PTIwJmM9NjJJX3B4/ZExfZ3VQZmpXSzA1/VXlKbzIxWVNNQ29f/aDB5bnNjNm5IWmgz/bz0"
            alt="" class="w-10 h-10 object-cover rounded-full" />
          <button class="flex justify-center items-center gap-2 bg-gray-200 py-2 rounded-full font-semibold w-full">
            <span>Search</span>
          </button>
        </div>
        <div class="navbar-button flex gap-2">
          <button class="flex justify-center items-center gap-2 bg-gray-200 px-2 py-2 rounded-full font-semibold">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
              stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
              class="icon icon-tabler icons-tabler-outline icon-tabler-calendar-plus">
              <path stroke="none" d="M0 0h24v24H0z" fill="none" />
              <path d="M12.5 21h-6.5a2 2 0 0 1 -2 -2v-12a2 2 0 0 1 2 -2h12a2 2 0 0 1 2 2v5" />
              <path d="M16 3v4" />
              <path d="M8 3v4" />
              <path d="M4 11h16" />
              <path d="M16 19h6" />
              <path d="M19 16v6" />
            </svg>
          </button>
          <button class="flex justify-center items-center gap-2 bg-gray-200 px-2 py-2 rounded-full font-semibold">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="currentColor"
              class="icon icon-tabler icons-tabler-filled icon-tabler-layout">
              <path stroke="none" d="M0 0h24v24H0z" fill="none" />
              <path d="M8 3a3 3 0 0 1 3 3v1a3 3 0 0 1 -3 3h-2a3 3 0 0 1 -3 -3v-1a3 3 0 0 1 3 -3z" />
              <path d="M8 12a3 3 0 0 1 3 3v3a3 3 0 0 1 -3 3h-2a3 3 0 0 1 -3 -3v-3a3 3 0 0 1 3 -3z" />
              <path d="M18 3a3 3 0 0 1 3 3v12a3 3 0 0 1 -3 3h-2a3 3 0 0 1 -3 -3v-12a3 3 0 0 1 3 -3z" />
            </svg>
          </button>
          <button class="flex justify-center items-center gap-2 bg-gray-200 px-2 py-2 rounded-full font-semibold">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
              stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
              class="icon icon-tabler icons-tabler-outline icon-tabler-books">
              <path stroke="none" d="M0 0h24v24H0z" fill="none" />
              <path d="M5 4m0 1a1 1 0 0 1 1 -1h2a1 1 0 0 1 1 1v14a1 1 0 0 1 -1 1h-2a1 1 0 0 1 -1 -1z" />
              <path d="M9 4m0 1a1 1 0 0 1 1 -1h2a1 1 0 0 1 1 1v14a1 1 0 0 1 -1 1h-2a1 1 0 0 1 -1 -1z" />
              <path d="M5 8h4" />
              <path d="M9 16h4" />
              <path
                d="M13.803 4.56l2.184 -.53c.562 -.135 1.133 .19 1.282 .732l3.695 13.418a1.02 1.02 0 0 1 -.634 1.219l-.133 .041l-2.184 .53c-.562 .135 -1.133 -.19 -1.282 -.732l-3.695 -13.418a1.02 1.02 0 0 1 .634 -1.219l.133 -.041z" />
              <path d="M14 9l4 -1" />
              <path d="M16 16l3.923 -.98" />
            </svg>
          </button>

          <!-- Conditional rendering for mobile -->
          <button v-if="!isLoggedIn"
            class="flex justify-center items-center gap-2 bg-gray-200 px-2 py-2 rounded-full font-semibold"
            @click="showLoginPopup = true">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
              stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
              class="icon icon-tabler icons-tabler-outline icon-tabler-login-2">
              <path stroke="none" d="M0 0h24v24H0z" fill="none" />
              <path d="M9 8v-2a2 2 0 0 1 2 -2h7a2 2 0 0 1 2 2v12a2 2 0 0 1 -2 2h-7a2 2 0 0 1 -2 -2v-2" />
              <path d="M3 12h13l-3 -3" />
              <path d="M13 15l3 -3" />
            </svg>
          </button>

          <!-- Logout button when logged in (mobile) -->
          <button v-else class="flex justify-center items-center gap-2 bg-gray-200 px-2 py-2 rounded-full font-semibold"
            @click="handleLogout">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
              stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path stroke="none" d="M0 0h24v24H0z" fill="none" />
              <path d="M14 8v-2a2 2 0 0 0 -2 -2h-7a2 2 0 0 0 -2 2v12a2 2 0 0 0 2 2h7a2 2 0 0 0 2 -2v-2" />
              <path d="M7 12h14l-3 -3m0 6l3 -3" />
            </svg>
          </button>
        </div>
      </nav>
    </div>

    <!-- Add the LoginPopup component here with login success handler -->
    <LoginPopup :show="showLoginPopup" @close="showLoginPopup = false" @login-success="onLoginSuccess" />

    <router-view />
  </div>
</template>