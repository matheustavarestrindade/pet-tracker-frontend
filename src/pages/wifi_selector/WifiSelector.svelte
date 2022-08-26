<script lang="typescript">
    import { createEventDispatcher } from "svelte";
    import Title from "../../components/Title.svelte";
    import Selector from "./Selector.svelte";
    import type { INetwork } from "./WifiSelectorTypes";
    const onNetworkSelect = createEventDispatcher<{ select_network: INetwork }>();
</script>

<div id="wifi-selector">
    <Title title={"Selecione uma rede Wifi para configurar seu Pet-tracker"} />
    <Selector on:select_network={(e) => onNetworkSelect("select_network", e.detail)} />
</div>
