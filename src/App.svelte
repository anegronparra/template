<script>
    let firstName = '';
    let lastName = '';
    let postcardTitle = '';
    let titleColor = 'black';
    let message = '';
    let textColor = 'black';
    let textBoxColor = 'white';
    let backgroundImage = '';
    let postcards = [];

    let availableImages = [
        { name: 'None', url: '' },
        { name: 'Image 1', url: 'images/image1.jpg' },
        { name: 'Image 2', url: 'images/image2.jpg' },
        { name: 'Image 3', url: 'images/image3.jpg' },
        { name: 'Image 4', url: 'images/image4.jpg' },
        { name: 'Image 5', url: 'images/image5.jpg' },
        { name: 'Image 6', url: 'images/image6.jpg' },
    ];

    let selectedImage = availableImages[0].url; // Default to 'None'

    function savePostcard() {
        const newPostcard = {
            firstName,
            lastName,
            postcardTitle,
            titleColor,
            message,
            textColor,
            textBoxColor,
            backgroundImage: selectedImage
        };
        postcards = [...postcards, newPostcard];
        // Reset form fields each time you save a postcard
        firstName = '';
        lastName = '';
        postcardTitle = '';
        titleColor = 'black';
        message = '';
        textColor = 'black';
        textBoxColor = 'white';
        selectedImage = availableImages[0].url; 
    }
</script>

<main>
    <h1>WPI Virtual Postcard Designer</h1>
    <div id="postcard-design">
        <h2>Design Your Postcard</h2>
        <div class="name-input">
			<label style="margin-right: 32px;" class="aligned-label" for="first-name">Name:</label>
			<input type="text" bind:value={firstName}>
			<label class="aligned-label" for="last-name">Last Name:</label>
			<input type="text" bind:value={lastName}>
		</div>

		<div class="title-row">
			<label style="margin-right: 43px;" class="aligned-label" for="title">Title:</label>
			<input type="text" placeholder="Enter title..." bind:value={postcardTitle}>
			<label class="aligned-label" for="title-color">Select title color: </label>
			<select bind:value={titleColor}>
				<option value="black">Black</option>
				<option value="blue">Blue</option>
				<option value="red">Red</option>
				<option value="purple">Purple</option>
			</select>
		</div>
		
        <div class="postcard-text-row">  <label class="aligned-label" for="message">Message: </label>
			<textarea placeholder="Add your message here..." bind:value={message} rows="5"></textarea>
			<label class="aligned-label" for="message-color">Select message color: </label>
			<select bind:value={textColor}>
				<option value="black">Black</option>
				<option value="blue">Blue</option>
				<option value="red">Red</option>
				<option value="purple">Purple</option>
			</select>
		</div>		

        <div class="image-selection-container">  <div class="background-image-row">
            <label for="background-image">Background Image:</label>
            <select bind:value={selectedImage}>
                {#each availableImages as image}
                    <option value={image.url}>{image.name}</option>
                {/each}
            </select>
        </div>
        {#if selectedImage}
            <div class="image-preview">
                <img src={selectedImage} alt="Image Preview" style="max-width: 100%; max-height: 200px;">
            </div>
        {/if}
    </div>

    <button style="background-color: greenyellow;" on:click={savePostcard}>Save Postcard</button>
</div>

    <div id="created-postcards-container">
        <h2>Your Created Postcards</h2>
        <div id="created-postcards">
            {#each postcards as postcard}
    <div class="postcard" style="background-image: url({postcard.backgroundImage}); background-size: cover;">
					<div class="postcard-image-overlay" style="background-color: rgba(255, 255, 255, 0.6); padding: 15px; border-radius: 5px;">
						<p style="color: {postcard.titleColor};"><strong></strong> {postcard.postcardTitle}</p>
						<p style="color: {postcard.textColor};"><strong></strong> {postcard.message}</p>
						<p><strong>From:</strong> {postcard.firstName} {postcard.lastName}</p>
					</div>
				</div>
			{/each}
        </div>
    </div>
</main>

<style>
    :global(body) {
        background: indianred;
    }

    body {
        background: indianred;
        color: black;
        font-family: 'Roboto', sans-serif;
        margin: 3%;
    }

    .name-input, .title, .postcard-text, .background-image-select, button {
        margin-bottom: 10px;
		width: max-content;
    }

    .name-input label, .title input, .postcard-text textarea, .title select, .postcard-text select, .background-image-select select {
        display: block;
        margin-top: 5px;
    }

    #postcard-design {
        margin-top: 20px;
        background: lightgray;
        padding: 2%;
        border-radius: 6px;
    }

    #created-postcards-container {
        margin-top: 20px;
    }

    #created-postcards {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        grid-gap: 10px;
    }

    .postcard {
        border: 1px solid #ddd;
        border-radius: 5px;
        overflow: hidden;
        aspect-ratio: 1 / 1;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }

    .postcard-image-overlay {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        height: 100%; 
        background-color: rgba(255, 255, 255, 0.6); 
        padding: 15px; 
        border-radius: 5px;
    }

    .image-preview {
        margin-top: 10px;
    }

	.postcard p:first-child { 
        font-size: 30px; 
    }

	.name-input {
 		display: flex;
	}

	.name-input label, .name-input input {
 		margin-right: 10px;
	}

	.title-row {
  		display: flex; 
	}

	.title-row label, .title-row input, .title-row select {
  		margin-right: 10px; 
	}

	.title-row label {
		align-self: center;
	}

	.postcard-text-row {
  		display: flex; 
	}
	
	.postcard-text-row label, .postcard-text-row textarea, .postcard-text-row select {
  		margin-right: 10px;
  		align-self: center;
		}

		.aligned-label {
		display: inline-block;
		width: fit-content;
		text-align: right;
		white-space: nowrap; 
  		overflow: hidden;
	}

	.background-image-row {
	display: flex;
	}

	.background-image-row label, .background-image-row select {
	margin-right: 10px;
	align-self: center;
	}

</style>
