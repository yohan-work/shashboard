<template>
  <button :class="buttonClass" v-bind="$attrs">
    <slot />
  </button>
</template>

<script setup lang="ts">
interface Props {
  variant?:
    | "default"
    | "destructive"
    | "outline"
    | "secondary"
    | "ghost"
    | "link";
  size?: "default" | "sm" | "lg" | "icon";
}

const props = withDefaults(defineProps<Props>(), {
  variant: "default",
  size: "default",
});

const baseClasses =
  "inline-flex items-center justify-center whitespace-nowrap rounded-lg text-sm font-medium ring-offset-background transition-all duration-200 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-primary focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50";

const variantClasses = {
  default: "bg-primary text-primary-foreground hover:bg-primary/90 shadow-sm",
  destructive:
    "bg-destructive text-destructive-foreground hover:bg-destructive/90 shadow-sm",
  outline:
    "border border-border bg-background hover:bg-accent hover:text-accent-foreground",
  secondary:
    "bg-secondary text-secondary-foreground hover:bg-secondary/80 shadow-sm",
  ghost: "hover:bg-accent hover:text-accent-foreground",
  link: "text-primary underline-offset-4 hover:underline",
};

const sizeClasses = {
  default: "h-10 px-4 py-2",
  sm: "h-8 rounded-md px-3 text-xs",
  lg: "h-12 rounded-lg px-8",
  icon: "h-10 w-10",
};

const buttonClass = computed(() => {
  return `${baseClasses} ${variantClasses[props.variant]} ${
    sizeClasses[props.size]
  }`;
});
</script>
