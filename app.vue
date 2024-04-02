<template>
    <div>
        <NuxtLayout>
            <header>
                <nav class="flex justify-between bg-gray-900 text-white">
                    <div class="px-2 xl:px-8 py-5 flex w-full items-center">
                        <ul
                            class="hidden md:flex px-4 font-semibold font-heading space-x-6"
                        >
                            <li>
                                <NuxtLink to="/">Home</NuxtLink>
                            </li>
                            <li>
                                <NuxtLink to="/Student"
                                    >List Of Students</NuxtLink
                                >
                            </li>
                            <li>
                                <NuxtLink to="/products"
                                    >List Of Products</NuxtLink
                                >
                            </li>
                            <li>
                                <NuxtLink to="/diagram">diagram</NuxtLink>
                            </li>
                            <li></li>
                        </ul>
                    </div>
                </nav>
            </header>
            <NuxtPage />
        </NuxtLayout>
    </div>
</template>
