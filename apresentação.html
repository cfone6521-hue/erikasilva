<script>
/* =========================================
   NANO WEBGPU — ÉRIKA SILVA
   Fundo generativo rosa e violeta
========================================= */

(async function NanoWebGPU() {

    const canvas = document.getElementById("nano-webgpu");

    if (!canvas || !navigator.gpu) {
        console.info("WebGPU indisponível. Site funcionando normalmente.");
        return;
    }

    try {

        const adapter = await navigator.gpu.requestAdapter();

        if (!adapter) return;

        const device = await adapter.requestDevice();

        const context = canvas.getContext("webgpu");

        if (!context) return;

        const format = navigator.gpu.getPreferredCanvasFormat();

        context.configure({
            device,
            format,
            alphaMode: "premultiplied"
        });

        /* Redimensionamento */
        function resize() {

            const ratio = Math.min(
                window.devicePixelRatio || 1,
                2
            );

            canvas.width = Math.max(
                1,
                Math.floor(window.innerWidth * ratio)
            );

            canvas.height = Math.max(
                1,
                Math.floor(window.innerHeight * ratio)
            );
        }

        resize();

        window.addEventListener("resize", resize);

        /* Shader */
        const shaderCode = `

        struct Uniforms {
            resolution: vec2f,
            time: f32,
            padding: f32,
        }

        @group(0) @binding(0)
        var<uniform> u: Uniforms;

        struct VertexOutput {
            @builtin(position) position: vec4f,
            @location(0) uv: vec2f,
        }

        @vertex
        fn vertexMain(
            @builtin(vertex_index) index: u32
        ) -> VertexOutput {

            var positions = array<vec2f, 3>(
                vec2f(-1.0, -1.0),
                vec2f( 3.0, -1.0),
                vec2f(-1.0,  3.0)
            );

            var output: VertexOutput;

            let p = positions[index];

            output.position = vec4f(p, 0.0, 1.0);
            output.uv = p * 0.5 + 0.5;

            return output;
        }

        fn hash(p: vec2f) -> f32 {
            return fract(
                sin(dot(p, vec2f(127.1, 311.7)))
                * 43758.5453
            );
        }

        fn noise(p: vec2f) -> f32 {

            let i = floor(p);
            let f = fract(p);

            let a = hash(i);
            let b = hash(i + vec2f(1.0, 0.0));
            let c = hash(i + vec2f(0.0, 1.0));
            let d = hash(i + vec2f(1.0, 1.0));

            let smooth = f * f * (3.0 - 2.0 * f);

            return mix(
                mix(a, b, smooth.x),
                mix(c, d, smooth.x),
                smooth.y
            );
        }

        @fragment
        fn fragmentMain(
            input: VertexOutput
        ) -> @location(0) vec4f {

            let uv = input.uv;

            let aspect = u.resolution.x / u.resolution.y;

            let t = u.time;

            var p = (uv - 0.5) * vec2f(aspect, 1.0);

            /* Movimento orgânico */
            p += vec2f(
                sin(t * 0.35 + p.y * 2.5),
                cos(t * 0.28 + p.x * 2.0)
            ) * 0.07;

            /* Fontes de luz */
            let center1 = vec2f(
                sin(t * 0.28) * 0.42,
                cos(t * 0.35) * 0.24
            );

            let center2 = vec2f(
                cos(t * 0.22 + 1.5) * 0.38,
                sin(t * 0.31) * 0.32
            );

            let center3 = vec2f(
                sin(t * 0.19 + 3.0) * 0.30,
                cos(t * 0.25 + 2.0) * 0.30
            );

            let d1 = length(p - center1);
            let d2 = length(p - center2);
            let d3 = length(p - center3);

            let glow1 = exp(-d1 * 5.0);
            let glow2 = exp(-d2 * 6.0);
            let glow3 = exp(-d3 * 7.0);

            /* Paleta rosa e violeta */
            let pink = vec3f(1.0, 0.08, 0.42);
            let rose = vec3f(0.85, 0.12, 0.38);
            let violet = vec3f(0.55, 0.08, 1.0);

            var color = vec3f(0.0);

            color += pink * glow1 * 0.75;
            color += rose * glow2 * 0.55;
            color += violet * glow3 * 0.60;

            /* Textura suave */
            let grain = noise(uv * 14.0 + t * 0.12);

            color += vec3f(0.04, 0.015, 0.03) * grain;

            /* Partículas */
            let grid = uv * u.resolution / 38.0;

            let cell = floor(grid);
            let local = fract(grid) - 0.5;

            let random = hash(cell);

            let distance = length(local);

            let particle = 1.0 - smoothstep(
                0.0,
                0.045,
                distance
            );

            let sparkle = step(0.985, random);

            let flicker = 0.5 + 0.5 * sin(
                t * 2.0 + random * 25.0
            );

            color += vec3f(1.0, 0.35, 0.65)
                * particle
                * sparkle
                * flicker;

            /* Vinheta */
            let vignette = 1.0 - smoothstep(
                0.15,
                0.85,
                length(p)
            );

            color *= vignette;

            /* Tonemapping */
            color = color / (1.0 + color);

            return vec4f(color, 1.0);
        }

        `;

        const shader = device.createShaderModule({
            code: shaderCode
        });

        /* Buffer de animação */
        const uniformBuffer = device.createBuffer({
            size: 16,
            usage:
                GPUBufferUsage.UNIFORM |
                GPUBufferUsage.COPY_DST
        });

        const bindGroupLayout =
            device.createBindGroupLayout({
                entries: [{
                    binding: 0,
                    visibility: GPUShaderStage.FRAGMENT,
                    buffer: {
                        type: "uniform"
                    }
                }]
            });

        const bindGroup = device.createBindGroup({
            layout: bindGroupLayout,
            entries: [{
                binding: 0,
                resource: {
                    buffer: uniformBuffer
                }
            }]
        });

        /* Pipeline gráfico */
        const pipeline = device.createRenderPipeline({

            layout: device.createPipelineLayout({
                bindGroupLayouts: [bindGroupLayout]
            }),

            vertex: {
                module: shader,
                entryPoint: "vertexMain"
            },

            fragment: {
                module: shader,
                entryPoint: "fragmentMain",
                targets: [{
                    format
                }]
            },

            primitive: {
                topology: "triangle-list"
            }
        });

        /* Animação */
        const startTime = performance.now();

        function render() {

            if (!canvas.isConnected) return;

            const time = (performance.now() - startTime) / 1000;

            device.queue.writeBuffer(
                uniformBuffer,
                0,
                new Float32Array([
                    canvas.width,
                    canvas.height,
                    time,
                    0
                ])
            );

            const encoder = device.createCommandEncoder();

            const pass = encoder.beginRenderPass({

                colorAttachments: [{
                    view: context
                        .getCurrentTexture()
                        .createView(),

                    clearValue: {
                        r: 0,
                        g: 0,
                        b: 0,
                        a: 0
                    },

                    loadOp: "clear",
                    storeOp: "store"
                }]
            });

            pass.setPipeline(pipeline);
            pass.setBindGroup(0, bindGroup);
            pass.draw(3);
            pass.end();

            device.queue.submit([
                encoder.finish()
            ]);

            requestAnimationFrame(render);
        }

        render();

        console.info("Nano WebGPU iniciado com sucesso.");

    } catch (error) {

        console.error("Erro ao iniciar WebGPU:", error);

    }

})();
</script>
