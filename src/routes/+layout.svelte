<script>
    import "../app.pcss";
    import { Button } from "flowbite-svelte";

</script>

<nav>
    <Button color="dark" shadow href="/">Home</Button>
    <Button color="dark" shadow href="/about">About</Button>
    <Button color="dark" shadow href="/todo">Todo</Button>
    <Button color="dark" shadow href="/auth">Auth</Button>
</nav>

<style>
    nav {
        background-color: var(--color-bg);
        padding: 1rem;
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 1rem;
    }
</style>

<slot></slot>