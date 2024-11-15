To run this implementation, load the above JSON file in ComfyUI and install all required custom nodes using 'Manager'! and then just run 'Queue Prompt' !

•	Created a small application for Video-to-Video transformation using Comfy UI’s custom nodes

•	Application took a MP4 video as input, transformed this according to user’s positive & negative prompt & generated an output MP4 video. Following components were used in building this:
1. Load Video(custom block): This block is used to import the original video that you want to transform. It loads each frame into the pipeline, making them accessible for subsequent processing steps.
2. Load Checkpoint: Loads the pre-trained model checkpoint, which contains the weights and architecture needed for the specific transformations. This checkpoint often determines the style or type of transformation (e.g., artistic style, anime style).
3. Load VAE (klf8anime): Loads a specific VAE (Variational Autoencoder) model, which is particularly useful for high-quality image generation in styles like anime. The VAE helps encode and decode images (or video frames in this case) into a more manageable latent space.
4. Load ControlNet Model (Canny) (custom block): Loads a ControlNet model that is trained to understand canny edges, a type of edge detection. This helps the model focus on the structural outline of objects in frames, which can guide the transformation to maintain the original video’s form.
5. CannyEdge: Applies the Canny edge detection algorithm to each frame. It detects edges within the frame, which helps emphasize structure and shape when feeding the frames into the ControlNet model for consistent and stable transformations.
6. Positive & Negative Prompt Blocks: Define the specific prompts for the transformation. The Positive Prompt guides the model on what to focus on or include in the transformation (e.g., "anime-style forest"). The Negative Prompt tells the model what to avoid or reduce, such as undesired details or artifacts (e.g., "blurry, low-quality").
7. VAE Encode: Encodes each video frame into the latent space using the VAE model. This compresses frame information into a lower-dimensional representation, which helps with efficient and effective transformations in the latent space.
8. Apply ControlNet (Advanced): Applies the ControlNet model to the encoded latent frames. This model uses the Canny edge information to guide the transformation and ensure that structural consistency is maintained across frames. This keeps the generated video coherent and stable.
9. KSampler Advanced: Samples from the latent space to create transformed images based on the control signals (prompts and ControlNet guidance). This is where the actual transformation or "stylization" of each frame occurs. Used advanced options to get greater control over parameters like denoising, which can affect the overall look.
10. VAE Decode: Decodes the transformed latent frames back into the pixel space, turning them into standard video frames with the new style or transformations applied.
11. Frame Interpolator: Smooths the transitions between frames, helping to avoid "jitter" or "flicker" that might occur in the transformed video. This ensures that the video plays smoothly and consistently.
12. SaveVideo: Takes the processed frames and compiles them into a final video file, saving it in the desired output format and location.

Sample demo done on:
Input used: A MP4 video of dancing skeleton
Output expected: Same dancing video but skeleton replaced by an anime girl with pink braided hair

