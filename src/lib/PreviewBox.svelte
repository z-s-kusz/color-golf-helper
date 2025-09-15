<script>
    let { label, colorRange } = $props();

    let style = $derived.by(() => {
        if (label.includes('mid')) {
            return getTestRange(label, colorRange);
        }

        let r = label.includes('R') ? colorRange.rMax : colorRange.rMin;
        let g = label.includes('G') ? colorRange.gMax : colorRange.gMin;
        let b = label.includes('B') ? colorRange.bMax : colorRange.bMin;
        return `background-color: rgb(${r}, ${g}, ${b});`;
    });

    function getTestRange(type, colors) {
        let percentile = 1;
        if (type === 'mid-high') percentile = 0.75;
        else if (type === 'mid-low') percentile = 0.25;
        else if (type === 'mid') percentile = 0.5;
        else console.error('unsupported label', label);

        // x = percentile * (max - min) + min
        let r = Math.floor((colors.rMax - colors.rMin) * percentile + colors.rMax);
        let g = Math.floor((colors.gMax - colors.gMin) * percentile + colors.gMax);
        let b = Math.floor((colors.bMax - colors.bMin) * percentile + colors.bMax);
        return `background-color: rgb(${r}, ${g}, ${b});`;
    }
</script>

<section>
    <div class="preview" style={style}></div>
    <h4>{label}</h4>
</section>

<style>
    h4 {
        margin: 0;
    }
    section {
        margin-bottom: 1.5rem;
    }
    .preview {
        height: 108px;
        width: 140px;
        border: 2px solid black;
    }
</style>
