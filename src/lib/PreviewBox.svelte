<script>
    let { label, colorRange } = $props();

    let style = $derived.by(() => {
        let r = '';
        let g = '';
        let b = '';

        if (label.includes('mid')) {
            let percentile = 1;
            if (label === 'mid-high') percentile = 0.75;
            else if (label === 'mid-low') percentile = 0.25;
            else if (label === 'mid') percentile = 0.5;
            else console.error('unsupported label', label);

            // x = percentile * (max - min) + min
            r = Math.floor((colorRange.rMax - colorRange.rMin) * percentile + colorRange.rMax);
            g = Math.floor((colorRange.gMax - colorRange.gMin) * percentile + colorRange.gMax);
            b = Math.floor((colorRange.bMax - colorRange.bMin) * percentile + colorRange.bMax);
        }

        r = label.includes('R') ? colorRange.rMax : colorRange.rMin;
        g = label.includes('G') ? colorRange.gMax : colorRange.gMin;
        b = label.includes('B') ? colorRange.bMax : colorRange.bMin;
        return `background-color: rgb(${r}, ${g}, ${b});`;
    });
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
