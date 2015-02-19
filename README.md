# MultipleImagePicker
Custom Gallery for Single and Multiple image pick



Usage
====
Firstly set your AndroidManifest.xml

<div class="highlight highlight-xml"><pre>
 &lt;<span class="pl-ent">activity</span> <span class="pl-e">android</span><span class="pl-e">:</span><span class="pl-e">name</span>=<span class="pl-s1"><span class="pl-pds">"</span>com.cunoraz.pickImages.CustomGalleryActivity<span class="pl-pds">"</span></span> &gt;
            &lt;<span class="pl-ent">intent-filter</span>&gt;
                &lt;<span class="pl-ent">action</span> <span class="pl-e">android</span><span class="pl-e">:</span><span class="pl-e">name</span>=<span class="pl-s1"><span class="pl-pds">"</span>cunoraz.ACTION_PICK<span class="pl-pds">"</span></span> /&gt;
                &lt;<span class="pl-ent">action</span> <span class="pl-e">android</span><span class="pl-e">:</span><span class="pl-e">name</span>=<span class="pl-s1"><span class="pl-pds">"</span>cunoraz.ACTION_MULTIPLE_PICK<span class="pl-pds">"</span></span> /&gt;

                &lt;<span class="pl-ent">category</span> <span class="pl-e">android</span><span class="pl-e">:</span><span class="pl-e">name</span>=<span class="pl-s1"><span class="pl-pds">"</span>android.intent.category.DEFAULT<span class="pl-pds">"</span></span> /&gt;
            &lt;/<span class="pl-ent">intent-filter</span>&gt;
 &lt;/<span class="pl-ent">activity</span>&gt;</pre></div>
 

        //Calling galery for sinle image
        Intent i = new Intent(Action.ACTION_PICK);
				startActivityForResult(i, 100);
				
        //Calling galery for multiple image
				Intent i = new Intent(Action.ACTION_MULTIPLE_PICK);
				startActivityForResult(i, 200);

 Overrie your activity's onActivityResult method like this
 
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
        imagePaths = new ArrayList<String>();
		if (requestCode == 100 && resultCode == Activity.RESULT_OK) {
			adapter.clear();

			viewSwitcher.setDisplayedChild(1);
			String single_path = data.getStringExtra("single_path");
            imagePaths.add(single_path);
			imageLoader.displayImage("file://" + single_path, imgSinglePick);

		} else if (requestCode == 200 && resultCode == Activity.RESULT_OK) {
			String[] all_path = data.getStringArrayExtra("all_path");

			ArrayList<CustomGallery> dataT = new ArrayList<CustomGallery>();

			for (String string : all_path) {
				CustomGallery item = new CustomGallery();
				item.sdcardPath = string;
                imagePaths.add(string);
				dataT.add(item);
			}

			viewSwitcher.setDisplayedChild(0);
			adapter.addAll(dataT);
		}
	}
SS
====
 <img src = "http://i.imgur.com/AJR6uD8.png"</img>
