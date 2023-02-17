<script>
    export let data;
    export let dim;
    import { format } from "d3";

    const formatComma = format(",");
</script>

<div class="tooltip" style="position:absolute; top:{dim.y}px; left:{dim.x}px">
    <p class="state-label"> <strong>{data.state}</strong></p>
    <p>Wind Turbines: <strong>{formatComma(data.wind_turbines)}</strong></p>
    <p>Installed Capacity (mw): <strong>{formatComma(data.installed_capacity_mw)}</strong></p>
    <p>Total Investment ($mn): <strong>{formatComma(data.total_investment_mn)}</strong></p>
    <p>Equivalent homes powered: <strong>{formatComma(data.equivalent_homes_powered)}</strong></p>

</div>

<style>
    .tooltip {
        padding: 20px;
        border: 1px solid rgb(0, 0, 0);
        pointer-events: none;
        transition: top 300ms, left 300ms;
        width: fit-content;
        border: 1px solid rgb(80, 80, 80);
        background: white;
        border-radius: 4px;
    }

    p {
        margin-bottom: 8px;
        color: rgb(80, 80, 80);
    }

    .state-label {
        font-size: 1.5rem;
        font-weight: bold;
        margin-bottom: 16px;
        color: black;
    }

    strong {
        color: black;
    }
</style>