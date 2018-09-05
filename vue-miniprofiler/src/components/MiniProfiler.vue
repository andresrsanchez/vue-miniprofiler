<template>
    <button type="button" @click="getProfiler">Click Me!</button> 
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import axios from 'axios';

@Component
export default class MiniProfiler extends Vue {
    private readonly key: string = 'MiniProfiler';
    private miniProfiler: any = (window as any)[this.key];

    @Prop() private id!: string;
    @Prop() private scriptSrc!: string;
    @Prop() private cssSrc!: string;
    @Prop() private dataPath!: string;
    @Prop({ default: '' }) private dataVersion!: string;
    @Prop({ default: 'right' }) private dataPosition!: string;
    @Prop({ default: true }) private dataChildren!: boolean;
    @Prop({ default: 35 }) private dataMaxTraces!: number;
    @Prop({ default: true }) private dataAuthorized!: boolean;
    @Prop({ default: false }) private dataStartHidden!: string;
    @Prop({ default: 'Alt+P' }) private dataToggleShortcut!: string;
    @Prop({ default: 35 }) private dataTrivialMilliseconds!: number;
    @Prop({ default: true }) private dataTrivial!: boolean;
    @Prop({ default: true }) private dataControls!: boolean;
    @Prop({ default: '' }) private dataCurrentId!: string;
    @Prop({ default: '' }) private dataIds!: string;
    @Prop({ default: true }) private scriptAsync!: boolean;
    @Prop({ default: '' }) private innerHTML!: string;

    private getProfiler() {
        axios.get('http://localhost:5000/api/values');
    }

    private created() {
        this.appendDivElement();
        this.appendCssLink();
    }

    private appendDivElement(): void {
        const body = document.body as HTMLDivElement;
        const script = document.createElement('script');
        script.innerHTML = this.innerHTML;
        script.src = this.scriptSrc;
        script.setAttribute('data-version', this.dataVersion);
        script.setAttribute('data-path', this.dataPath);
        script.setAttribute('data-position', this.dataPosition);
        script.setAttribute('id', this.id);
        script.setAttribute('data-current-id', this.dataCurrentId);
        script.setAttribute('data-ids', this.dataIds);
        script.setAttribute('data-trivial', this.dataTrivial.toString());
        script.setAttribute('data-children', this.dataChildren.toString());
        script.setAttribute('data-max-traces', this.dataMaxTraces.toString());
        script.setAttribute('data-controls', this.dataControls.toString());
        script.setAttribute('data-authorized', this.dataAuthorized.toString());
        script.setAttribute('data-start-hidden', this.dataStartHidden.toString());
        script.setAttribute('data-toggle-shortcut', this.dataToggleShortcut);
        script.setAttribute('data-trivial-milliseconds', this.dataTrivialMilliseconds.toString());
        script.async = this.scriptAsync;

        body.appendChild(script);
    }

    private appendCssLink(): void {
        const body = document.body as HTMLDivElement;
        const css = document.createElement('link');
        const cssUrl = this.cssSrc;
        css.href = cssUrl;
        css.rel = 'stylesheet';

        body.appendChild(css);
    }
}
</script>