<script>
    let yourStakedPear = 100000;
    let totalStakedPear = 100000000;
    let feesPercentage = 0.13;
    let pearProtcolVolumePerDay = 10000000;
    let feesForStaked = 0.80;

    $: dailyDividend = (((pearProtcolVolumePerDay * (feesPercentage / 100)) * 0.80) / totalStakedPear) * yourStakedPear;
    $: monthlyDividend = dailyDividend * 30;
    $: yearlyDividend = dailyDividend * 365;
    $: yourPercentageOfStakedPear = yourStakedPear / totalStakedPear * 100;

    // Function to format currency with 2 decimals
    function formatCurrency(value) {
        const formatter = new Intl.NumberFormat('en-US');
        return `$${formatter.format(value.toFixed(2))}`;
    }

    // Function to format percentage with 2 decimals
    function formatPercentage(value, decimals = 2) {
        return `${value.toFixed(decimals)}%`;
    }
</script>

<div class="bg-bg-grey p-0 md:p-10 flex min-h-screen font-primary font-thin">
    <div class="bg-white w-full flex flex-col 2xl:flex-row justify-between md:rounded-[20px] 2xl:rounded-[40px] overflow-hidden shadow-md/10">
        <div class="bg-light-grey w-full flex flex-col justify-center 2xl:justify-start 2xl:max-w-[300px] h-[80px] 2xl:h-full border-b 2xl:border-b-0 2xl:border-r border-bg-grey py-4 2xl:py-20 px-5 md:px-10">
            <h1 class="text-xl md:text-3xl">Staking<strong class="text-primary">Pear</strong></h1>
            <div class="hidden 2xl:flex mt-4">
                <p>More options coming soon!</p>
            </div>
        </div>
        <div class="w-full">
            <div class="px-5 py-10 md:px-10 md:p-10 2xl:p-20">
                <div class="w-full max-w-[900px]">
                    <h2 class="text-2xl md:text-4xl font-normal">PEAR Dividend Calculator - Estimate Your Rewards</h2>
                    <div class="mt-4">
                        <p>Easily calculate your PEAR token dividend based on the exchange's trading volume and your staked tokens. Enter your holdings and see your potential earnings instantly!</p>
                        <p class="font-bold mt-2">NOTE: Users pay fees when opening trades, so volume is based on trade openings.</p>
                    </div>
                </div>

                <div class="mt-10 flex flex-col gap-5 md:gap-10">
                    <div class="flex flex-col gap-2">
                        <span class="text-lg font-normal">The amount of staked pear tokens (<span class="font-bold">{formatCurrency(yourStakedPear)}</span>)</span>
                        <div class="flex gap-4 items-center flex-col md:flex-row">
                            <input class="w-full md:max-w-[500px] h-2 bg-primary rounded-lg appearance-none cursor-pointer dark:bg-primary" type="range" bind:value={yourStakedPear} min="0" max="560000000" step="1">
                            <input class="border border-black/20 py-2 px-4 rounded-md w-full md:max-w-[200px]" bind:value={yourStakedPear} type="number" min="0" max={totalStakedPear} step="1">
                        </div>
                    </div>

                    <div class="flex flex-col gap-2 mt-5">
                        <span class="text-lg font-normal">The total staked Pear tokens exclude 44% that will never circulate. Max staked: 560M (<span class="font-bold">{formatCurrency(totalStakedPear)}</span>)</span>
                        <div class="flex gap-4 items-center flex-col md:flex-row">
                            <input class="w-full md:max-w-[500px] h-2 bg-primary rounded-lg appearance-none cursor-pointer dark:bg-primary" type="range" bind:value={totalStakedPear} min={yourStakedPear} max="560000000" step="1">
                            <input class="border border-black/20 py-2 px-4 rounded-md w-full md:max-w-[200px]" bind:value={totalStakedPear} type="number" min="0" max="560000000" step="1">
                        </div>
                    </div>

                    <div class="flex flex-col gap-2 mt-5">
                        <span class="text-lg font-normal">Fees percentage (<span class="font-bold">{feesPercentage}%</span>)</span>
                        <div class="flex gap-4 items-center flex-col md:flex-row">
                            <input class="w-full md:max-w-[500px] h-2 bg-primary rounded-lg appearance-none cursor-pointer dark:bg-primary" type="range" bind:value={feesPercentage} min="0.01" max="0.20" step="0.01">
                            <input class="border border-black/20 py-2 px-4 rounded-md w-full md:max-w-[200px]" bind:value={feesPercentage} type="number" min="0" max="0.20" step="0.01">
                        </div>
                    </div>

                    <div class="flex flex-col gap-2 mt-5">
                        <span class="text-lg font-normal">Pear Protcol Volume per day (<span class="font-bold">{formatCurrency(pearProtcolVolumePerDay)}</span>)</span>
                        <div class="flex gap-4 items-center flex-col md:flex-row">
                            <input class="w-full md:max-w-[500px] h-2 bg-primary rounded-lg appearance-none cursor-pointer dark:bg-primary" type="range" bind:value={pearProtcolVolumePerDay} min="0" max="1000000000" step="100000">
                            <input class="border border-black/20 py-2 px-4 rounded-md w-full md:max-w-[200px]" bind:value={pearProtcolVolumePerDay} type="number" min="0" step="1">
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="w-full 2xl:max-w-[530px] bg-light-grey border-l border-bg-grey py-10 2xl:py-20 px-5 md:px-10 flex flex-col gap-5">
            <div class="flex flex-col border-b pb-5 border-black/10">
                <h3 class="text-lg">Daily dividend</h3>
                <span class="mt-1 text-3xl">{formatCurrency(dailyDividend)}</span>
            </div>
            <div class="flex flex-col border-b pb-5 border-black/10">
                <h3 class="text-lg">Montly dividend</h3>
                <span class="mt-1 text-3xl">{formatCurrency(monthlyDividend)}</span>
            </div>
            <div class="flex flex-col border-b pb-5 border-black/10">
                <h3 class="text-lg">Yearly dividend</h3>
                <span class="mt-1 text-3xl">{formatCurrency(yearlyDividend)}</span>
            </div>
            <div class="flex flex-col border-b pb-5 border-black/10">
                <h3 class="text-lg">Staked percentage</h3>
                <span class="mt-1 text-3xl">{formatPercentage(yourPercentageOfStakedPear)}</span>
            </div>
        </div>
    </div>
</div>