<template>
    <div style="width: 100%; height: 80vh">
        <canvas id="acquisitions"></canvas>
    </div>
</template>

<script>
import Chart from "chart.js/auto";

(async function () {
    const data = [
        { year: "Q3", count: 30 },
        { year: "Q4", count: 22 },
        { year: "Q1", count: 47 },
        { year: "Q2", count: 20 },
        { year: "Q3", count: 26 },
        { year: "Q4", count: 10 },
        { year: "Q1", count: 15 },
        { year: "Q2", count: 21 },
    ];
    new Chart(document.getElementById("acquisitions"), {
        type: "line",
        data: {
            labels: data.map((row) => row.year),
            datasets: [
                {
                    label: "Acquisitions by year",
                    data: data.map((row) => row.count),
                    tension: 0.05,
                    borderColor: "lime",
                },
            ],
        },
    });
})();
</script>
