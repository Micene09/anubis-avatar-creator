<template>
<div class="container">
	<div class="page">
		<div id="title" class="title-bar">
			<h3 class="title">Anubis Avatar Creator</h3>
			<span class="tools">
				<ThemeSwitch />
				<GitHubRepo :href="repoUrl" class="contrast" />
			</span>
		</div>
		<div class="form" id="form">
			<ColorPicker label="Background" v-model="bgcolor" />
			<ColorPicker label="Body" v-model="body" />
			<ColorPicker label="Body lights" v-model="bodyLights" />
			<ColorPicker label="Primary" v-model="primary" />
			<ColorPicker label="Secondary" v-model="secondary" />
			<div class="grid">
				<Presets @update:modelValue="onPresetChanged" />
				<div class="grid">
					<label>
						&nbsp;
						<button class="outline" @click="onClickImport"><small>Import</small></button>
					</label>
					<label>
						&nbsp;
						<button class="outline" @click="onClickExport"><small>Export</small></button>
					</label>
				</div>
			</div>
			<div class="grid">
				<ResolutionPicker v-model:w="width" v-model:h="height" :disabled="format === 'SVG'" />
				<label class="just-button">
					&nbsp;
					<button class="outline" @click="onClickRandomColors">Random Colors</button>
				</label>
			</div>
			<div class="save-area">
				<label>
					&nbsp;
					<button :data-tooltip="copiedTooltip" @click="share">Share</button>
				</label>
				<label>
					&nbsp;
					<button @click="download">Export as</button>
				</label>
				<FormatPicker label="&nbsp;" v-model="format" />
			</div>
		</div>
		<div class="logo-wrapper" id="preview" :style="{ background: bgcolor }" :aria-busy="loadingDebounced">
			<template v-if="!loadingDebounced">
				<Logo class="logo"
					:body="body"
					:body-lights="bodyLights"
					:primary="primary"
					:secondary="secondary"
				/>
				<Logo class="logo chat small"
					:body="body"
					:body-lights="bodyLights"
					:primary="primary"
					:secondary="secondary"
					:style="{ background: bgcolor }"
				/>
				<Logo class="logo chat extra-small"
					:body="body"
					:body-lights="bodyLights"
					:primary="primary"
					:secondary="secondary"
					:style="{ background: bgcolor }"
				/>
			</template>
		</div>
	</div>
</div>
<div class="print-area" ref="printArea" :style="{
		background: bgcolor,
		width: width + 'px',
		height: height + 'px'
	}">
	<Logo class="logo"
		:body="body"
		:body-lights="bodyLights"
		:primary="primary"
		:secondary="secondary"
	/>
</div>
</template>
<script lang="ts" src="./app.ts" />
