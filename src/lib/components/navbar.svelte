<script lang="ts">
    import { createEventDispatcher } from 'svelte';
    import { slide } from 'svelte/transition';

    export let activeTab: 'application' |'volunteer' | 'about' | 'info' | 'sponsors' | 'rsvp' | 'theme-and-tracks' = 'application';

    const dispatch = createEventDispatcher();
    let isMenuOpen = false;

    function setTab(tab: 'application' | 'volunteer' | 'about' | 'info' | 'sponsors' | 'rsvp' | 'theme-and-tracks') {
        activeTab = tab;
        dispatch('change', tab);
        isMenuOpen = false;
    }
</script>

<nav class="w-full z-20 relative backdrop-blur-md bg-black/20 border-b border-white/10" aria-label="Main Navigation">
    <!-- Desktop Menu -->
    <div class="hidden xl:flex justify-center items-center gap-4 py-4 px-8">
        <button 
            class="nav-btn {activeTab === 'application' ? 'active' : ''}" 
            on:click={() => setTab('application')}
            aria-current={activeTab === 'application' ? 'page' : undefined}
        >
            Application
        </button>
        <!--<button 
            class="nav-btn {activeTab === 'rsvp' ? 'active' : ''}" 
            on:click={() => setTab('rsvp')}
            aria-current={activeTab === 'rsvp' ? 'page' : undefined}
        >
            RSVP
        </button>-->
        <button
            class="nav-btn {activeTab === 'volunteer' ? 'active' : ''}" 
            on:click={() => setTab('volunteer')}
            aria-current={activeTab === 'volunteer' ? 'page' : undefined}
        >
            Volunteer
        </button>
        <button 
            class="nav-btn {activeTab === 'about' ? 'active' : ''}" 
            on:click={() => setTab('about')}
            aria-current={activeTab === 'about' ? 'page' : undefined}
        >
            About
        </button>
        <button 
            class="nav-btn {activeTab === 'info' ? 'active' : ''}" 
            on:click={() => setTab('info')}
            aria-current={activeTab === 'info' ? 'page' : undefined}
        >
            Info and FAQ
        </button>
        <button 
            class="nav-btn {activeTab === 'theme-and-tracks' ? 'active' : ''}" 
            on:click={() => setTab('theme-and-tracks')}
            aria-current={activeTab === 'theme-and-tracks' ? 'page' : undefined}
        >
            Theme & Tracks
        </button>
        <button 
            class="nav-btn {activeTab === 'sponsors' ? 'active' : ''}" 
            on:click={() => setTab('sponsors')}
            aria-current={activeTab === 'sponsors' ? 'page' : undefined}
        >
            Sponsors
        </button>
    </div>

    <!-- Mobile Menu Header -->
    <div class="xl:hidden flex justify-between items-center py-4 px-6">
        <button 
            class="text-white focus:outline-none hover:text-[#C5A059] transition-colors" 
            on:click={() => isMenuOpen = !isMenuOpen}
            aria-label={isMenuOpen ? "Close menu" : "Open menu"}
            aria-expanded={isMenuOpen}
            aria-controls="mobile-menu"
        >
            <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24" aria-hidden="true">
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
        <div id="mobile-menu" class="xl:hidden flex flex-col items-center pb-6 gap-4 border-t border-white/5 bg-black/10" transition:slide>
            <button 
                class="nav-btn {activeTab === 'application' ? 'active' : ''}" 
                on:click={() => setTab('application')}
                aria-current={activeTab === 'application' ? 'page' : undefined}
            >
                Application
            </button>
            <!--<button 
                class="nav-btn {activeTab === 'rsvp' ? 'active' : ''}" 
                on:click={() => setTab('rsvp')}
                aria-current={activeTab === 'rsvp' ? 'page' : undefined}
            >
                RSVP
            </button>-->
            <button
            class="nav-btn {activeTab === 'volunteer' ? 'active' : ''}" 
            on:click={() => setTab('volunteer')}
            aria-current={activeTab === 'volunteer' ? 'page' : undefined}
            >
                Volunteer
            </button>
            <button 
                class="nav-btn {activeTab === 'about' ? 'active' : ''}" 
                on:click={() => setTab('about')}
                aria-current={activeTab === 'about' ? 'page' : undefined}
            >
                About
            </button>
            <button 
                class="nav-btn {activeTab === 'info' ? 'active' : ''}" 
                on:click={() => setTab('info')}
                aria-current={activeTab === 'info' ? 'page' : undefined}
            >
                Info and FAQ
            </button>
            <button 
                class="nav-btn {activeTab === 'theme-and-tracks' ? 'active' : ''}" 
                on:click={() => setTab('theme-and-tracks')}
                aria-current={activeTab === 'theme-and-tracks' ? 'page' : undefined}
            >
                Theme & Tracks
            </button>
            <button 
                class="nav-btn {activeTab === 'sponsors' ? 'active' : ''}" 
                on:click={() => setTab('sponsors')}
                aria-current={activeTab === 'sponsors' ? 'page' : undefined}
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
