<script>
    import BurgerMenuLogo from "./BurgerMenuLogo.svelte";
    import Cancel from "./Cancel.svelte";
    export let links;

    import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();

    let isMenuOpen = false;

    const handleClick = () => {
        isMenuOpen = !isMenuOpen;
        //document.body.classList.toggle("burger-menu-visible", isMenuOpen);
        isMenuOpen ? dispatch("onmenuopen") : dispatch("onmenuclose");
    }

</script>

<div class="burger-menu">
    <button class="burger-menu_btn" on:click={handleClick}>
        {#if isMenuOpen}
            <Cancel />
        {:else}
            <BurgerMenuLogo />
        {/if}
    </button>
    <div class={isMenuOpen ? 'burger-links' : 'burger-links hidden'}>
        <ul class="burger-menu_links-1">
            {#each links as link}
                {#if link.id === 1 || link.id === 2 || link.id === 3}
                    <li class="dropdown-item" style="text-decoration: none;">
                        <a href={link.url} class="nav-link">{link.text}</a>
                    </li>
                {/if}
            {/each}
        </ul>
        <ul class="burger-menu_links-2">
            {#each links as link}
                {#if link.id !== 1 && link.id !== 2 && link.id !== 3}
                    <li class="dropdown-item" style="text-decoration: none;">
                        <a href={link.url} class="nav-link">{link.text}</a>
                    </li>
                {/if}
            {/each}
        </ul>
    </div>
</div>

<style>
    .burger-menu {
        display: none;
        padding: 0 1px;
    }

    .burger-menu_btn {
        margin-left: 10px;
    }

    button {
        background: none;
        cursor: pointer;
    }

    .burger-links {
        display: flex;
        justify-content: space-between;
        position: absolute;
        z-index: 10;
        top: 40px;
        left: calc((-100vw + var(--reduced-width)) / 2);
        width: 100vw;
        height: 8rem;
        background-color: rgba(255, 255, 255, 0.8);
        border-bottom-left-radius: var(--border-radius);
        border-bottom-right-radius: var(--border-radius);
    }

    .burger-menu_links-1,
    .burger-menu_links-2 {
        display: block;
        margin-top: 1rem;
    }

    .burger-menu_links-1 {
        margin-left: calc((100vw - var(--reduced-width)) / 2);
        width: auto;
    }

    .burger-menu_links-2 {
        margin-right: calc((100vw - var(--reduced-width)) / 2);
        width: auto;
    }

    .dropdown-item {
        list-style-type: none;
        margin-bottom: 0.75rem;
    }

    .nav-link {
        font-family: var(--font-inter);
        font-size: 3.125vw;
        text-decoration: none;
        color: var(--dark-grey);
    }

    .nav-link:hover,
    .nav-links:active {
        background-color: var(--green);
        background-image: var(--gradient);
        background-size: 100%;
        -webkit-background-clip: text;
        -moz-background-clip: text;
        -webkit-text-fill-color: transparent; 
        -moz-text-fill-color: transparent;
    }

    @media (width < 480px) {
        .burger-menu {
            display: block;
        }

        .hidden {
            display: none;
        }
    }
</style>