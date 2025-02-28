<template>
    <div>
        <nav class="flex justify-between items-center px-8 md:px-12 lg:px-32 xl:px-48 py-4 bg-gray-400">
            <div class="navbar-utility flex gap-2">
                <img src="https://imgs.search.brave.com/5z3y1_Y3lst6b4j7yo9x-jS0MJ5yQZmmLUHNDcCDdkU/rs:fit:860:0:0:0/g:ce/aHR0cHM6Ly9tZWRp/YS5pc3RvY2twaG90/by5jb20vaWQvMTM0/NDMyMzUyOC9waG90/by9zaG90LW9mLWEt/eW91bmctYnVzaW5l/c3NtYW4td29ya2lu/Zy1vbi1hLWNvbXB1/dGVyLWluLWFuLW9m/ZmljZS5qcGc_cz02/MTJ4NjEyJnc9MCZr/PTIwJmM9NjJJX3B4/ZExfZ3VQZmpXSzA1/VXlKbzIxWVNNQ29f/aDB5bnNjNm5IWmgz/bz0"
                    alt="" class="w-10 h-10 object-cover rounded-full" />
                <button class="flex justify-center items-center gap-2 bg-gray-200 px-4 py-2 rounded-full font-semibold">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                        stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                        class="icon icon-tabler icons-tabler-outline icon-tabler-search">
                        <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                        <path d="M10 10m-7 0a7 7 0 1 0 14 0a7 7 0 1 0 -14 0" />
                        <path d="M21 21l-6 -6" />
                    </svg>
                    <span>Search</span>
                </button>
                <div class="bg-gray-200 flex justify-center items-center gap-3 px-4 py-2 rounded-full font-semibold">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                        stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                        class="icon icon-tabler icons-tabler-outline icon-tabler-calendar-plus">
                        <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                        <path d="M12.5 21h-6.5a2 2 0 0 1 -2 -2v-12a2 2 0 0 1 2 -2h12a2 2 0 0 1 2 2v5" />
                        <path d="M16 3v4" />
                        <path d="M8 3v4" />
                        <path d="M4 11h16" />
                        <path d="M16 19h6" />
                        <path d="M19 16v6" />
                    </svg>
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                        fill="currentColor" class="icon icon-tabler icons-tabler-filled icon-tabler-layout">
                        <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                        <path d="M8 3a3 3 0 0 1 3 3v1a3 3 0 0 1 -3 3h-2a3 3 0 0 1 -3 -3v-1a3 3 0 0 1 3 -3z" />
                        <path d="M8 12a3 3 0 0 1 3 3v3a3 3 0 0 1 -3 3h-2a3 3 0 0 1 -3 -3v-3a3 3 0 0 1 3 -3z" />
                        <path d="M18 3a3 3 0 0 1 3 3v12a3 3 0 0 1 -3 3h-2a3 3 0 0 1 -3 -3v-12a3 3 0 0 1 3 -3z" />
                    </svg>
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                        stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                        class="icon icon-tabler icons-tabler-outline icon-tabler-books">
                        <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                        <path d="M5 4m0 1a1 1 0 0 1 1 -1h2a1 1 0 0 1 1 1v14a1 1 0 0 1 -1 1h-2a1 1 0 0 1 -1 -1z" />
                        <path d="M9 4m0 1a1 1 0 0 1 1 -1h2a1 1 0 0 1 1 1v14a1 1 0 0 1 -1 1h-2a1 1 0 0 1 -1 -1z" />
                        <path d="M5 8h4" />
                        <path d="M9 16h4" />
                        <path
                            d="M13.803 4.56l2.184 -.53c.562 -.135 1.133 .19 1.282 .732l3.695 13.418a1.02 1.02 0 0 1 -.634 1.219l-.133 .041l-2.184 .53c-.562 .135 -1.133 -.19 -1.282 -.732l-3.695 -13.418a1.02 1.02 0 0 1 .634 -1.219l.133 -.041z" />
                        <path d="M14 9l4 -1" />
                        <path d="M16 16l3.923 -.98" />
                    </svg>
                </div>
            </div>
            <div class="navbar-button">
                <button class="flex justify-center items-center gap-2 bg-gray-200 px-4 py-2 rounded-full font-semibold">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                        stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                        class="icon icon-tabler icons-tabler-outline icon-tabler-login-2">
                        <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                        <path d="M9 8v-2a2 2 0 0 1 2 -2h7a2 2 0 0 1 2 2v12a2 2 0 0 1 -2 2h-7a2 2 0 0 1 -2 -2v-2" />
                        <path d="M3 12h13l-3 -3" />
                        <path d="M13 15l3 -3" />
                    </svg>
                    <span>Sign In</span>
                </button>
            </div>
        </nav>
        <div class="content px-8 md:px-12 lg:px-32 xl:px-48 py-4">
            <div class="grid grid-cols-8 w-full gap-8">
                <div class="col-span-8 2xl:col-span-6">
                    <div class="comic-info md:flex gap-8">
                        <div class="comic-cover w-fit">
                            <img src="https://assets.bwbx.io/images/users/iqjWHBFdfxIU/i3sY5OlfH3mc/v1/340x260.jpg"
                                class="min-w-56 max-w-56 h-80 object-cover rounded-lg" alt="">
                        </div>
                        <div class="comic-detail">
                            <h1 class="text-6xl font-bold">The DeepSeek Competitors Vying to Be China’s Next AI Champion
                            </h1>
                            <div class="detail-tags mt-4 flex gap-2">
                                <span
                                    class="inline-flex items-center rounded-md bg-green-50 px-2 py-1 text-sm font-medium text-green-700 ring-1 ring-green-600/20 ring-inset">Ongoing</span>
                                <span
                                    class="inline-flex gap-2 items-center rounded-md bg-gray-50 px-2 py-1 text-sm font-medium text-gray-600 ring-1 ring-gray-500/10 ring-inset">
                                    <img src="https://imgs.search.brave.com/8cnLO-1k9cSqfKc0AzHje3mjsXrPbnKUdhwLUpx3FIc/rs:fit:500:0:0:0/g:ce/aHR0cHM6Ly9pbWcu/ZnJlZXBpay5jb20v/cHJlbWl1bS1waG90/by9mbGFnLWNoaW5h/LWNoaW5hLWZsYWct/Y2hpbmVzZS1mbGFn/XzEwNDMzNy0xMDIw/NS5qcGc_c2VtdD1h/aXNfaHlicmlk"
                                        class="w-5 h-5 object-cover object-left rounded-full" alt="">
                                    <span>News</span>
                                </span>
                                <span
                                    class="inline-flex gap-2 items-center rounded-md bg-gray-50 px-2 py-1 text-sm font-medium text-gray-600 ring-1 ring-gray-500/10 ring-inset">
                                    <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24"
                                        fill="currentColor"
                                        class="icon icon-tabler icons-tabler-filled icon-tabler-clock-hour-4">
                                        <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                                        <path
                                            d="M17 3.34a10 10 0 1 1 -15 8.66l.005 -.324a10 10 0 0 1 14.995 -8.336m-5 2.66a1 1 0 0 0 -1 1v5.026l.009 .105l.02 .107l.04 .129l.048 .102l.046 .078l.042 .06l.069 .08l.088 .083l.083 .062l3 2a1 1 0 1 0 1.11 -1.664l-2.555 -1.704v-4.464a1 1 0 0 0 -.883 -.993z" />
                                    </svg>
                                    <span>Feb 26, 2025</span>
                                </span>
                                <span
                                    class="inline-flex gap-2 items-center rounded-md bg-gray-50 px-2 py-1 text-sm font-medium text-gray-600 ring-1 ring-gray-500/10 ring-inset">
                                    <span>Information</span>
                                </span>
                            </div>
                            <div
                                class="detail-description mt-4 bg-gray-50 px-4 py-2 rounded-lg ring 1 ring-gray-500/10 ring-inset">
                                The next DeepSeek to disrupt the global artificial intelligence industry could also come
                                from China.
                                <br><br>
                                The country of 1.4 billion has seeded several promising AI startups and projects, while
                                its leading internet players have spent years investing and developing the
                                infrastructure to support such new ventures. With the DeepSeek experience casting doubt
                                over the need for bleeding-edge expensive AI hardware from the likes of Nvidia Corp. —
                                which the US has banned from sale in China — the prospects of China’s up-and-coming AI
                                companies look to be improving.
                                <br><br>
                                Here are the rising companies and services to keep an eye on, as Chinese businesses get
                                creative in navigating trade curbs and developing more efficient AI models. The
                                valuations are derived from Pitchbook data and previous Bloomberg News reporting.
                            </div>
                            <div class="flex h-10 gap-2 mt-4">
                                <button
                                    class="px-3 py-2 bg-gray-50 ring-1 ring-gray-500/10 ring-inset rounded-lg flex justify-center items-center gap-2">
                                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                        fill="currentColor"
                                        class="icon icon-tabler icons-tabler-filled icon-tabler-player-play">
                                        <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                                        <path
                                            d="M6 4v16a1 1 0 0 0 1.524 .852l13 -8a1 1 0 0 0 0 -1.704l-13 -8a1 1 0 0 0 -1.524 .852z" />
                                    </svg>
                                    <span>Start Reading</span>
                                </button>
                                <button
                                    class="px-3 py-2 bg-gray-50 ring-1 ring-gray-500/10 ring-inset rounded-lg flex justify-center items-center gap-2">
                                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                        fill="currentColor"
                                        class="icon icon-tabler icons-tabler-filled icon-tabler-player-play">
                                        <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                                        <path
                                            d="M6 4v16a1 1 0 0 0 1.524 .852l13 -8a1 1 0 0 0 0 -1.704l-13 -8a1 1 0 0 0 -1.524 .852z" />
                                    </svg>
                                    <span>New Chapter</span>
                                </button>
                                <div
                                    class="divider mx-2 w-1 h-full rounded-full bg-gray-50 ring-1 ring-gray-500/10 ring-inset">
                                </div>
                                <button
                                    class="px-10 py-2 bg-gray-50 ring-1 ring-gray-500/10 ring-inset rounded-lg flex justify-center items-center gap-2">
                                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                        fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                        stroke-linejoin="round"
                                        class="icon icon-tabler icons-tabler-outline icon-tabler-plus">
                                        <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                                        <path d="M12 5l0 14" />
                                        <path d="M5 12l14 0" />
                                    </svg>
                                    <span>Add to Library</span>
                                </button>
                                <button
                                    class="px-3 py-2 bg-gray-50 ring-1 ring-gray-500/10 ring-inset rounded-lg flex justify-center items-center gap-2">
                                    <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24"
                                        fill="currentColor"
                                        class="icon icon-tabler icons-tabler-filled icon-tabler-bell">
                                        <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                                        <path
                                            d="M14.235 19c.865 0 1.322 1.024 .745 1.668a3.992 3.992 0 0 1 -2.98 1.332a3.992 3.992 0 0 1 -2.98 -1.332c-.552 -.616 -.158 -1.579 .634 -1.661l.11 -.006h4.471z" />
                                        <path
                                            d="M12 2c1.358 0 2.506 .903 2.875 2.141l.046 .171l.008 .043a8.013 8.013 0 0 1 4.024 6.069l.028 .287l.019 .289v2.931l.021 .136a3 3 0 0 0 1.143 1.847l.167 .117l.162 .099c.86 .487 .56 1.766 -.377 1.864l-.116 .006h-16c-1.028 0 -1.387 -1.364 -.493 -1.87a3 3 0 0 0 1.472 -2.063l.021 -.143l.001 -2.97a8 8 0 0 1 3.821 -6.454l.248 -.146l.01 -.043a3.003 3.003 0 0 1 2.562 -2.29l.182 -.017l.176 -.004z" />
                                    </svg>
                                </button>
                            </div>
                        </div>
                    </div>
                    <div class="comic-socials mt-8 grid grid-cols-2 gap-3">
                        <div class="col-span-2">
                            <div
                                class="p-2 py-3 h-16 bg-gray-50 ring-1 ring-gray-500/10 ring-inset rounded-lg flex items-center">
                                <div
                                    class="divider mx-2 w-1 h-full rounded-full bg-gray-200 ring-1 ring-gray-500/10 ring-inset">
                                </div>
                                <div class="flex flex-col">
                                    <p>Share Kumapage</p>
                                    <span class="text-sm">to your friends</span>
                                </div>
                            </div>
                        </div>
                        <div class="col-span-1">
                            <div
                                class="p-2 py-3 h-16 bg-gray-50 ring-1 ring-gray-500/10 ring-inset rounded-lg flex items-center justify-between">
                                <div class="h-full flex items-center">
                                    <div
                                        class="divider mx-2 mr-4 w-1 h-full rounded-full bg-gray-200 ring-1 ring-gray-500/10 ring-inset">
                                    </div>
                                    <div class="flex flex-col">
                                        <p class="text-lg">Share Kumapage</p>
                                        <span class="text-sm">to your friends</span>
                                    </div>
                                </div>
                                <button class="px-4 py-2 bg-red-400 rounded-full text-white flex items-center gap-2">
                                    <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24"
                                        fill="currentColor"
                                        class="icon icon-tabler icons-tabler-filled icon-tabler-alert-hexagon">
                                        <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                                        <path
                                            d="M10.425 1.414a3.33 3.33 0 0 1 3.026 -.097l.19 .097l6.775 3.995l.096 .063l.092 .077l.107 .075a3.224 3.224 0 0 1 1.266 2.188l.018 .202l.005 .204v7.284c0 1.106 -.57 2.129 -1.454 2.693l-.17 .1l-6.803 4.302c-.918 .504 -2.019 .535 -3.004 .068l-.196 -.1l-6.695 -4.237a3.225 3.225 0 0 1 -1.671 -2.619l-.007 -.207v-7.285c0 -1.106 .57 -2.128 1.476 -2.705l6.95 -4.098zm1.585 13.586l-.127 .007a1 1 0 0 0 0 1.986l.117 .007l.127 -.007a1 1 0 0 0 0 -1.986l-.117 -.007zm-.01 -8a1 1 0 0 0 -.993 .883l-.007 .117v4l.007 .117a1 1 0 0 0 1.986 0l.007 -.117v-4l-.007 -.117a1 1 0 0 0 -.993 -.883z" />
                                    </svg>
                                    <span>Report</span>
                                </button>
                            </div>
                        </div>
                        <div class="col-span-1">
                            <div
                                class="p-2 py-3 h-16 bg-gray-50 ring-1 ring-gray-500/10 ring-inset rounded-lg flex items-center justify-between">
                                <div class="h-full flex items-center">
                                    <div
                                        class="divider mx-2 w-1 h-full rounded-full bg-gray-200 ring-1 ring-gray-500/10 ring-inset">
                                    </div>
                                    <div class="flex flex-col">
                                        <p>Share Kumapage</p>
                                        <span class="text-sm">to your friends</span>
                                    </div>
                                </div>
                                <button class="px-4 py-2 bg-red-400 rounded-full text-white flex items-center gap-2">
                                    <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24"
                                        fill="currentColor"
                                        class="icon icon-tabler icons-tabler-filled icon-tabler-alert-hexagon">
                                        <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                                        <path
                                            d="M10.425 1.414a3.33 3.33 0 0 1 3.026 -.097l.19 .097l6.775 3.995l.096 .063l.092 .077l.107 .075a3.224 3.224 0 0 1 1.266 2.188l.018 .202l.005 .204v7.284c0 1.106 -.57 2.129 -1.454 2.693l-.17 .1l-6.803 4.302c-.918 .504 -2.019 .535 -3.004 .068l-.196 -.1l-6.695 -4.237a3.225 3.225 0 0 1 -1.671 -2.619l-.007 -.207v-7.285c0 -1.106 .57 -2.128 1.476 -2.705l6.95 -4.098zm1.585 13.586l-.127 .007a1 1 0 0 0 0 1.986l.117 .007l.127 -.007a1 1 0 0 0 0 -1.986l-.117 -.007zm-.01 -8a1 1 0 0 0 -.993 .883l-.007 .117v4l.007 .117a1 1 0 0 0 1.986 0l.007 -.117v-4l-.007 -.117a1 1 0 0 0 -.993 -.883z" />
                                    </svg>
                                    <span>Report</span>
                                </button>
                            </div>
                        </div>
                    </div>
                    <div class="comic-episodes mt-6">
                        <div class="episodes-info flex justify-between items-center">
                            <p class="text-2xl font-semibold">100 Chapters</p>
                            <button>
                                <svg xmlns="http://www.w3.org/2000/svg" width="42" height="42" viewBox="0 0 24 24"
                                    fill="none" stroke="currentColor" stroke-width="1" stroke-linecap="round"
                                    stroke-linejoin="round"
                                    class="icon icon-tabler icons-tabler-outline icon-tabler-sort-descending-numbers">
                                    <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                                    <path d="M4 15l3 3l3 -3" />
                                    <path d="M7 6v12" />
                                    <path d="M17 14a2 2 0 0 1 2 2v3a2 2 0 1 1 -4 0v-3a2 2 0 0 1 2 -2z" />
                                    <path d="M17 5m-2 0a2 2 0 1 0 4 0a2 2 0 1 0 -4 0" />
                                    <path d="M19 5v3a2 2 0 0 1 -2 2h-1.5" />
                                </svg>
                            </button>
                        </div>
                        <div class="episodes-list grid grid-cols-3 gap-4 mt-6">
                            <div class="bg-gray-50 ring-1 ring-gray-500/10 ring-inset rounded-lg p-2 flex items-center">
                                <div class="flex items-center gap-4">
                                    <img src="https://assets.bwbx.io/images/users/iqjWHBFdfxIU/ixfNTiyYtG1c/v0/459x306.webp"
                                        alt="" class="h-full w-36 rounded-lg">
                                    <div class="flex flex-col">
                                        <p class="font-semibold text-lg">Chapter 100</p>
                                        <span>Feb 27, 2025</span>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="comic-comments mt-6 bg-gray-200 h-96 rounded-lg flex justify-center items-center">
                        <button
                            class="bg-gray-50 ring-1 ring-gray-500/10 ring-inset flex items-center gap-2 rounded-lg px-6 py-2">
                            <svg xmlns="http://www.w3.org/2000/svg" width="28" height="28" viewBox="0 0 24 24"
                                fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                stroke-linejoin="round"
                                class="icon icon-tabler icons-tabler-outline icon-tabler-messages">
                                <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                                <path d="M21 14l-3 -3h-7a1 1 0 0 1 -1 -1v-6a1 1 0 0 1 1 -1h9a1 1 0 0 1 1 1v10" />
                                <path d="M14 15v2a1 1 0 0 1 -1 1h-7l-3 3v-10a1 1 0 0 1 1 -1h2" />
                            </svg>
                            <span class="text-lg font-semibold">Click to load comments</span>
                        </button>
                    </div>
                </div>
                <div class="col-span-2 hidden 2xl:block">
                    <div class="other-comics">
                        <div
                            class="bg-gray-50 ring-1 ring-gray-500/10 ring-inset p-4 rounded-lg flex items-center gap-4">
                            <img src="https://assets.bwbx.io/images/users/iqjWHBFdfxIU/i3sY5OlfH3mc/v1/340x260.jpg"
                                class="min-w-20 max-w-20 h-28 object-cover rounded-lg" alt="">
                            <span class="text-3xl font-bold">1</span>
                            <div class="flex flex-col gap-2">
                                <p class="text-lg">The DeepSeek Competitors Vying to Be China's</p>
                                <span class="text-sm">Drama</span>
                                <div class="flex gap-2">
                                    <span
                                        class="inline-block rounded-md bg-gray-50 px-2 py-1 text-sm font-medium text-gray-600 ring-1 ring-gray-500/10 ring-inset whitespace-nowrap">
                                        <span>Information</span>
                                    </span>
                                    <span
                                        class="inline-block rounded-md bg-gray-50 px-2 py-1 text-sm font-medium text-gray-600 ring-1 ring-gray-500/10 ring-inset whitespace-nowrap">
                                        <span>Information</span>
                                    </span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Detail',
}
</script>