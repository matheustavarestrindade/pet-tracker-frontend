<script lang="ts">
    import BackButton from "./components/BackButton.svelte";

    import Container from "./components/Container.svelte";
    import Footer from "./components/Footer.svelte";
    import WifiConnection from "./pages/wifi_connection/WifiConnection.svelte";
    import WifiSelector from "./pages/wifi_selector/WifiSelector.svelte";
    import type { INetwork } from "./pages/wifi_selector/WifiSelectorTypes";

    let selected_network: INetwork | undefined = undefined;
    // let selected_network: INetwork | undefined = {
    //     has_password: true,
    //     ssid: "",

    // };

    const onNetworkSelect = (event: CustomEvent<INetwork>) => {
        selected_network = event.detail;
    };

    const onBack = () => {
        selected_network = undefined;
    };
</script>

<div id="app">
    <Container>
        {#if selected_network == undefined}
            <WifiSelector on:select_network={onNetworkSelect} />
        {/if}
        {#if selected_network != undefined}
            <BackButton on:click={onBack} />
            <WifiConnection selectedNetwork={selected_network} />
        {/if}
    </Container>
    <Footer />
</div>

<style>
    #app {
        min-height: 100vh;
        display: flex;
        flex-direction: column;
    }
</style>
