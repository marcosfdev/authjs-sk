<script lang="ts">
  import { page } from "$app/stores";
  import { SignIn, SignOut } from "@auth/sveltekit/components";
  import "../app.css";
  import star from '$lib/assets/star.png';
</script>

<header>
  <nav class="bg-white shadow">
    <div class="max-w-7xl mx-auto px-4 lg:px-8">
      <div class="flex justify-between items-center py-3">
        <!-- Left section for logo and navigation links -->
        <div class="flex items-center space-x-4">
          <img alt="star logo" src={star} />
           <nav class="hidden lg:flex space-x-8">
            <a href="/" class="border-b-2 border-indigo-500 text-base font-medium text-gray-900 px-1 pt-1">Home</a>
            <a href="/protected" class="border-b-2 border-transparent text-base font-medium text-gray-500 hover:border-gray-300 hover:text-gray-700 px-1 pt-1">Protected</a>
          </nav>
        </div>

        <!-- Right section for user authentication and avatar -->
        <div class="flex items-center space-x-4">
          {#if $page.data.session}
            <span class="text-base leading-6">{$page.data.session.user?.email ?? $page.data.session.user?.name}</span>
            <SignOut>
              <button class="bg-indigo-500 hover:bg-indigo-400 text-white font-semibold py-2 px-4 rounded-md shadow focus:outline-none">Sign out</button>
            </SignOut>
          {:else}
            <span class="text-base leading-6">You are not signed in</span>
            <SignIn>
              <button class="bg-blue-500 hover:bg-blue-400 text-white font-semibold py-2 px-4 rounded-md shadow focus:outline-none">Sign in</button>
            </SignIn>
            <img class="ml-4 h-10 w-10 rounded-full" src={$page.data?.session?.user?.image ?? "https://source.boringavatars.com/marble/120"} alt="User avatar">
          {/if}
        </div>
      </div>
    </div>
  </nav>
</header>

<style>
  header nav {
    width: 100%; /* Ensures full width */
    background-color: #fff; /* White background */
    box-shadow: 0 2px 4px rgba(0,0,0,0.1); /* Subtle shadow for depth */
  }
</style>
