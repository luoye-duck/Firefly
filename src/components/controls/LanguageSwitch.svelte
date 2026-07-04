<script lang="ts">
import { onMount } from "svelte";
import DropdownItem from "@/components/common/DropdownItem.svelte";
import DropdownPanel from "@/components/common/DropdownPanel.svelte";
import Icon from "@/components/common/Icon.svelte";

const LANGUAGES = [
	{ code: "zh_CN", label: "简体中文", flag: "🇨🇳" },
	{ code: "zh_TW", label: "繁體中文", flag: "🇭🇰" },
	{ code: "en", label: "English", flag: "🇺🇸" },
	{ code: "ja", label: "日本語", flag: "🇯🇵" },
];

let currentLang = $state("zh_CN");

function switchLang(code: string) {
	currentLang = code;
	localStorage.setItem("user-lang", code);
	document.documentElement.lang = code;
	window.dispatchEvent(
		new CustomEvent("language-change", { detail: { lang: code } }),
	);
	// 关闭面板
	const panel = document.getElementById("lang-switch-panel");
	if (panel) panel.classList.add("float-panel-closed");
}

onMount(() => {
	const stored = localStorage.getItem("user-lang") || "zh_CN";
	currentLang = stored;
	document.documentElement.lang = stored;

	// Swup 页面切换后重新读取
	const handleContentReplace = () => {
		const lang = localStorage.getItem("user-lang") || "zh_CN";
		currentLang = lang;
	};

	const win = window as any;
	if (win.swup?.hooks) {
		win.swup.hooks.on("content:replace", handleContentReplace);
	} else {
		document.addEventListener("swup:enable", () => {
			if (win.swup?.hooks) {
				win.swup.hooks.on("content:replace", handleContentReplace);
			}
		});
	}
});
</script>

<div class="relative z-50">
	<button
		aria-label="Language"
		aria-haspopup="menu"
		class="relative btn-plain scale-animation rounded-lg h-11 w-11 active:scale-90"
		id="lang-switch-btn"
	>
		<div class="absolute inset-0 flex items-center justify-center">
			<span class="text-[1.4rem] leading-none">
				{LANGUAGES.find((l) => l.code === currentLang)?.flag ?? "🌐"}
			</span>
		</div>
	</button>
	<div
		id="lang-switch-panel"
		class="absolute transition float-panel-closed top-11 -right-2 pt-5 z-50"
		role="menu"
		aria-labelledby="lang-switch-btn"
	>
		<DropdownPanel>
			{#each LANGUAGES as lang, i (lang.code)}
				<DropdownItem
					role="menuitem"
					isActive={currentLang === lang.code}
					isLast={i === LANGUAGES.length - 1}
					onclick={() => switchLang(lang.code)}
				>
					<span class="text-base mr-1.5 leading-none">{lang.flag}</span>
					<span class="text-sm font-medium mr-3">{lang.label}</span>
					{#if currentLang === lang.code}
						<Icon
							icon="material-symbols:check-rounded"
							class="text-[1rem] ml-auto text-(--primary)"
						></Icon>
					{/if}
				</DropdownItem>
			{/each}
		</DropdownPanel>
	</div>
</div>
