<script lang="ts">
    import "../app.css";
    import Header from "$lib/Header.svelte";
    import SideNav from "$lib/SideNav.svelte";
    import Footer from "$lib/Footer.svelte";
    import { onDestroy, onMount } from 'svelte';

    let lastScrollY = 0;
    let headerVisible = true;

    const handleScroll = () => {
        const currentScrollY = window.scrollY;
        console.log("Current Scroll Y:", currentScrollY);
        console.log("Last Scroll Y:", lastScrollY);

        if (currentScrollY > lastScrollY) {
            // Scrolling down
            headerVisible = false;
        } else {
            // Scrolling up
            headerVisible = true;
        }
        console.log("Header Visible:", headerVisible);

        lastScrollY = currentScrollY;
    };

    onMount(() => {
        if (typeof window !== 'undefined') {
            lastScrollY = window.scrollY;
            window.addEventListener('scroll', handleScroll);
        }
    });

    onDestroy(() => {
        if (typeof window !== 'undefined') {
            window.removeEventListener('scroll', handleScroll);
        }
    });
</script>

<style>
    .fixed-sidebar {
        position: fixed;
        top: 0;
        bottom: 0;
        overflow-y: auto;
    }
    :global(body) {
        background-color: #F4F6F8;
    }

    .flex.h-screen {
        min-height: 100vh;
        background-color: #F4F6F8;

    }

    .flex-col-adjusted {
    width: calc(100% - 5rem); /* Assuming the sidebar width (w-20) is 5rem */
    margin-left: 5rem; /* Adjust the margin-left to match the sidebar width */
  }
</style>

<div class="flex h-screen">
    <div class="fixed-sidebar">
        <SideNav />
    </div>
    <div class="flex flex-col flex-col-adjusted"> <!-- Adjust margin-left to match SideNav width -->
        <Header isVisible={headerVisible} />
        <main class="flex-1">
            <slot />
        </main>
        <Footer />
    </div>
</div>