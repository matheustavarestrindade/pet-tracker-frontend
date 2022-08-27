<script lang="ts">
    import { createEventDispatcher, onMount } from "svelte";
    import Loader from "../../components/Loader.svelte";
    import Title from "../../components/Title.svelte";
    import Selector from "./Selector.svelte";
    import type { INetwork } from "./WifiSelectorTypes";
    const onNetworkSelect = createEventDispatcher<{ select_network: INetwork }>();
    let networks = [];
    const handleNetworksQuery = async () => {
        try {
            const response = await fetch("/query_networks");
            const jsonResponse = await response.json();
            networks = jsonResponse.networks;
        } catch (error) {
            console.error("Cannot query networks");
        }
    };
    onMount(async () => {
        const interval = setInterval(handleNetworksQuery, 10000);
        return () => clearInterval(interval);
    });
</script>

<div id="wifi-selector">
    <Title title={"Selecione uma rede Wifi para configurar seu Pet-tracker"} />
    {#if networks.length == 0}
        <Loader loadingText="Procurando redes..." />
    {:else}
        <Selector on:select_network={(e) => onNetworkSelect("select_network", e.detail)} {networks} />
    {/if}
</div>
