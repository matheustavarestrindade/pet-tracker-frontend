<script lang="typescript">
    import Title from "../../components/Title.svelte";
    import type { INetwork } from "../wifi_selector/WifiSelectorTypes";
    export let selectedNetwork: INetwork;
</script>

<div id="wifi-connection">
    <Title title={"Conectando a rede"} subtitle={selectedNetwork.ssid} />
    <div id="wifi-credentials">
        {#if selectedNetwork.has_password}
            <div id="password-input">
                <input type="password" placeholder="Digite a senha da rede Wifi" />
            </div>
        {/if}
        <button id="connect-button">Conectar</button>
    </div>
</div>

<style lang="scss">
    @import "../../styles/colors.scss";
    #wifi-connection {
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: column;
        #wifi-credentials {
            min-height: 50vh;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-direction: column;

            #connect-button {
                width: 100%;
                height: 50px;
                background-color: $base-color;
                color: white;
                border: none;
                outline: none;
                cursor: pointer;
                font-size: 1.5rem;
                font-weight: bold;
                transition: 0.2s;
                &:hover {
                    background-color: $base-color-light;
                }
            }

            #password-input {
                width: 100%;
                height: 50px;
                border-bottom: 2px solid $base-color;
                display: flex;
                align-items: center;
                justify-content: center;
                margin-bottom: 1rem;
                input {
                    width: 100%;
                    height: 100%;
                    border: none;
                    outline: none;
                    font-size: 1.2em;
                    font-weight: bold;
                    padding: 0 10px;
                    color: $text-color-light;
                }
            }
        }
    }
</style>
