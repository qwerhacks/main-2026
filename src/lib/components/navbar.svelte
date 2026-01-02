<script lang="ts">
    import { createEventDispatcher } from 'svelte';
    export let activeTab: 'application' | 'about' | 'sponsors' = 'application';

    const dispatch = createEventDispatcher();

    function setTab(tab: 'application' | 'about' | 'sponsors') {
        activeTab = tab;
        dispatch('change', tab);
    }
</script>

<div class="w-full flex justify-center items-center gap-4 py-4 z-20 relative backdrop-blur-md bg-black/20 border-b border-white/10">
    <button 
        class="nav-btn {activeTab === 'application' ? 'active' : ''}" 
        on:click={() => setTab('application')}
    >
        Application
    </button>
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
