<script lang="ts">
    import { createEventDispatcher } from 'svelte';
    import { slide } from 'svelte/transition';

    export let activeTab: 'application' | 'about' | 'sponsors' | 'rsvp' = 'application';

    const dispatch = createEventDispatcher();
    let isMenuOpen = false;

    function setTab(tab: 'application' | 'about' | 'sponsors' | 'rsvp') {
        activeTab = tab;
        dispatch('change', tab);
        isMenuOpen = false;
    }
</script>

<nav class="w-full z-20 relative backdrop-blur-md bg-black/20 border-b border-white/10">
    <!-- Desktop Menu -->
    <div class="hidden md:flex justify-center items-center gap-4 py-4 px-8">
        <button 
            class="nav-btn {activeTab === 'application' ? 'active' : ''}" 
            on:click={() => setTab('application')}
        >
            Application
        </button>
        <!--<button 
            class="nav-btn {activeTab === 'rsvp' ? 'active' : ''}" 
            on:click={() => setTab('rsvp')}
        >
            RSVP
        </button>-->
        <button 
            class="nav-btn {activeTab === 'about' ? 'active' : ''}" 
            on:click={() => setTab('about')}
        >
            About
        </button>
        <button 
            class="nav-btn {activeTab === 'sponsors' ? 'active' : ''}" 
            on:click={() => setTab('sponsors')}
        >
            Sponsors
        </button>
    </div>

    <!-- Mobile Menu Header -->
    <div class="md:hidden flex justify-between items-center py-4 px-6">
        <button 
            class="text-white focus:outline-none hover:text-[#C5A059] transition-colors" 
            on:click={() => isMenuOpen = !isMenuOpen}
            aria-label="Toggle menu"
        >
            <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                {#if isMenuOpen}
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                {:else}
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
                {/if}
            </svg>
        </button>
    </div>

    <!-- Mobile Dropdown -->
    {#if isMenuOpen}
        <div class="md:hidden flex flex-col items-center pb-6 gap-4 border-t border-white/5 bg-black/10" transition:slide>
            <button 
                class="nav-btn {activeTab === 'application' ? 'active' : ''}" 
                on:click={() => setTab('application')}
            >
                Application
            </button>
            <!--<button 
                class="nav-btn {activeTab === 'rsvp' ? 'active' : ''}" 
                on:click={() => setTab('rsvp')}
            >
                RSVP
            </button>-->
            <button 
                class="nav-btn {activeTab === 'about' ? 'active' : ''}" 
                on:click={() => setTab('about')}
            >
                About
            </button>
            <button 
                class="nav-btn {activeTab === 'sponsors' ? 'active' : ''}" 
                on:click={() => setTab('sponsors')}
            >
                Sponsors
            </button>
        </div>
    {/if}
</nav>

<style>
    .nav-btn {
        display: inline-block;
        background: transparent;
        color: white;
        font-family: 'Ranille Normal', serif;
        font-weight: bold;
        border: none;
        border-bottom: 2px solid transparent;
        padding: 0.5rem 1rem;
        text-align: center;
        text-transform: uppercase;
        cursor: pointer;
        transition: all 0.2s ease;
        font-size: 1.1rem;
    }

    .nav-btn:hover {
        color: #C5A059;
        transform: translateY(-2px);
    }

    .nav-btn.active {
        color: #C5A059;
        border-bottom: 2px solid #C5A059;
        text-shadow: 0 0 10px rgba(197, 160, 89, 0.5);
    }
</style>
