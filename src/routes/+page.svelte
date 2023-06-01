<script lang="ts">
	import { fade, fly } from 'svelte/transition';
	import MarkdownEditor from '\$/lib/components/MarkdownEditor.svelte';
	import { database, admin } from '\$/firebase';
	import { getDoc, collection, doc, orderBy, getDocs, query, setDoc, addDoc} from 'firebase/firestore';
	import { onMount } from 'svelte';
	import { getAuthApp } from '\$/firebase';
	import { each, query_selector_all } from 'svelte/internal';
	import SvelteMarkdown from 'svelte-markdown';
	import { dateSinceFormatter } from '$utils/dateSinceFormatter';


	let value = '# Post an Announcement';

	const auth = getAuthApp();

	let userDoc;

	let sortedAnnouncements;

	onMount(async () => {
		const db = database();
		const announcementsRef = collection(db, 'announcements');
		const querySnapshot = await getDocs(query(announcementsRef, orderBy('createdAt', 'desc')));
		
		const docRef = doc(db, 'users', auth.currentUser.uid);
    	const docSnap = await getDoc(docRef);
    	userDoc = docSnap.data();
		
		sortedAnnouncements = querySnapshot.docs.map((doc) => doc.data());
		console.log(sortedAnnouncements);

	});

	async function submit() {

		const db = database();
		const announcementsRef = collection(db, 'announcements');

		let announcement_data = {
			author: userDoc.first_name + ' ' + userDoc.last_name,
			content: value,
			createdAt: new Date(),
		};

		await addDoc(announcementsRef, announcement_data);
}

</script>

<div class="w-full p-2 bg-base-200 max-w-2xl">
	<div class='flex flex-col gap-2' in:fly={{ y: 50, duration: 400, delay: 100 }} out:fade={{ duration: 100 }}>

		<div class='bg-red-500 w-full h-100'>
			<img src='https://github.com/TristanCopley/delnorte-csa/assets/89225438/bc74339e-0ce7-45eb-88be-42ecec4a95d5' alt="bomb" width="656" height="450">
		</div>
		<br>
		<div class='font-bold'>Del Norte CSA Website Redone</div>
			<span>An easier and simpler way for Mr. Mortensen to interact with his students and for his students to interact with his content during the entire
				 school year for CSA. Del Norte Website Redone also provides a better and cleaner version of jupyter notebooks/github pages for documentation.</span>
		
		<div class='font-bold'>CTE Standards</div>
		<ul class="list-disc px-10">
			<li>C1.0 Identify and apply the systems development process.</li>
			<li>C1.1 Identify the phases of the systems development life cycle, including analysis, design, programming, testing, implementation, maintenance, and improvement.</li>
			<li>C1.2 Identify and describe models of systems development, software development life cycle (SDLC), and agile computing.</li>
			<li>C1.3 Identify and describe how specifications and requirements are developed for new and existing software applications.</li>
			<li>C1.4 Work as a member of, and within the scope and boundaries of, a development project team.</li>
			<li>C1.5 Track development project milestones using the concept of versions.</li>
		</ul>
		
				 <div class='w-full min-h-[28rem] max-h-[48rem] bg-base-300 px-2 py-2 overflow-y-scroll'>

			<span class="self-start text-xl font-bold">Teacher Announcements:</span>

			{#if sortedAnnouncements}

				{#each sortedAnnouncements as post }

					<div class="flex flex-col w-full min-h-[2rem] mt-4 justify-center bg-base-200">
						<article class="flex flex-row w-full h-full gap-2 prose px-4 pt-4">

							<div class="avatar self-center">
								<div class="w-10 rounded-full h-fit border border-lg border-base-300">
								<img src={auth.currentUser?.photoURL} />
								</div>
							</div>
							
							<span class="self-center text-sm">{post.author}</span>
							<span class="self-center text-sm opacity-30"> • </span>
							<span class="self-center text-sm opacity-30">{dateSinceFormatter(post.createdAt)}</span>

						</article>

						<div class="divider w-11/12 self-center"></div> 
						
						<div class="prose px-4 pb-4">
							<SvelteMarkdown source={post.content}/>
						</div>
					
				
					</div>

				{/each}

			{/if}

		</div>

		<div class='bg-base-100 w-full min-h-[10rem] rounded-md'>
			<MarkdownEditor bind:value={value}/>
			<button on:click={submit} class="btn btn-primary absolute right-3 bottom-3">Post</button>
		</div>

	</div>
</div>
