<script setup lang="ts">
import ProjectCard from '@/components/ProjectCard.vue';
import rawProjectData from '@/data/projects.json' with {type: 'json'};
import rawActivityList from 'virtual:activity-list.json' with {type: 'json'};
import rawNewsList from 'virtual:news-list.json' with {type: 'json'};
import type { Project } from '@/data/project';
import type { Activity } from '@/data/activity';
import type { News } from '@/data/news';
import ActivityListEntry from '@/components/ActivityListEntry.vue';
import NewsListEntry from '@/components/NewsListEntry.vue';
import AutoDarkImage from '@/components/AutoDarkImage.vue';

import LcpuDark from '../assets/lcpu-dark.svg';
import LcpuLight from '../assets/lcpu-light.svg';
import GithubMark from '../assets/github-mark.svg';
import GithubMarkWhite from '../assets/github-mark-white.svg';
import { ChevronRightIcon } from '@heroicons/vue/20/solid';

const projects = rawProjectData as Project[];
const activities = rawActivityList as Activity[];
const news = rawNewsList as News[];
</script>

<template>
  <main>
    <div w-full md:h-screen md:h-100dvh md:grid md:grid-cols-3 max-w-1680px m-x-auto>
      <div flex="~ items-center justify-center col" w-full h-full m-t-24 md:m-t-0>
        <AutoDarkImage h-48 :src="LcpuDark" :src-dark="LcpuLight" />
        <span m-t-8 text-3xl font-semibold>北京大学 Linux 俱乐部</span>
        <span m-t-1 text-lg>Linux Club of Peking University</span>
        <a href="https://github.com/lcpu-club" h-8 w-8 m-t-8>
          <AutoDarkImage :src="GithubMark" :src-dark="GithubMarkWhite" h-full w-full />
        </a>
      </div>
      <div col-span-2 p-x-6 p-y-12 md:p-x-12 overflow-auto>
        <h2>项目</h2>
        <div grid md:grid-cols-2 lg:grid-cols-3 gap-2>
          <ProjectCard v-for="project in projects" :key="project.title" :project="project" />
        </div>

        <div m-t-12 flex="~ items-center">
          <h2 flex-grow-1>活动</h2>
          <a class="text-unset! hover:bg-gray/10 p-l-2 p-y-1 rounded-md" decoration-none flex="~ items-center"
            href="/activities/">
            <span>所有活动</span>
            <ChevronRightIcon class="h-6" />
          </a>
        </div>

        <div>
          <ActivityListEntry v-for="activity in activities.slice(0, 3)" :key="activity.title" :activity="activity" />
        </div>

        <div m-t-12 flex="~ items-center">
          <h2 flex-grow-1>新闻</h2>
          <a class="text-unset! hover:bg-gray/10 p-l-2 p-y-1 rounded-md" decoration-none flex="~ items-center"
            href="/news/">
            <span>所有新闻</span>
            <ChevronRightIcon class="h-6" />
          </a>
        </div>
        <div>
          <NewsListEntry v-for="_news in news.slice(0, 3)" :key="_news.title" :news="_news" />
        </div>
      </div>
    </div>
  </main>
</template>

<style lang="css" scoped></style>
