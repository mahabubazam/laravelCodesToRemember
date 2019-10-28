# laravelCodesToRemember


//Code for Counting

	{{(App\User::all()->count())}}



// Edit

	function edit($user_id)
	    {
	      $single_data = User::findOrFail($user_id);
	      return view('users.edit',compact('single_data'));
	    }

//update

	function update(Request $request)
	    {
	      User::find($request->user_id)->update([
		'name'    =>$request->name,
		'email'    =>$request->email,
	      ]);
	      return back();
	    }
	
//delete

	function delete($user_id)
	    {
	      User::findOrFail($user_id)->delete();
	      return back();
	    }
    
//restore
    
    function restore_banner($banner_id)
      {
      User::onlyTrashed()->where('id',$user_id)->restore();
      return back();
    }
    
 
 
 
 //alert message
   
	   @if (session('success'))
	   <div class="alert alert-success">
	       {{ session('success') }}
	   </div>
	   @endif

 //error

                    @if ($errors->any())
                        <ul>
                        @foreach ($errors->all() as $error)
                        <div class="alert alert-danger">
                        <li>{{ $error }}</li>
                        </div>
                        @endforeach
                        </ul>
                    @endif
   
   
   
   // relationship
   
	   function relationbetweencategory()
	    {
	      return $this->hasOne('App\Category','id','category_id');
				// Category - id , product-category_id
	    }
   
   
   
   // photo upload
   
	   if ($request->hasFile('header_banner')) {
		$photo_upload     =  $request ->header_banner;
		$photo_extension  =  $photo_upload -> getClientOriginalExtension();
		$photo_name       =  $last_inserted_id . "." . $photo_extension;
		Image::make($photo_upload)->resize(1600,800)->save(base_path('public/uploads/banner/'.$photo_name),100);
		Banner::find($last_inserted_id)->update([
		'header_banner'          => $photo_name,
	      ]);
	      }


 // Photo Update
 
	   if($request->hasFile('header_banner')){
		if(Banner::find($request->banner_id)->header_banner=='default.png'){
		  $photo_upload     = $request->header_banner;
		  $photo_extension  =  $photo_upload->getClientOriginalExtension();
		  $photo_name       =  $request->header_banner . "." . $photo_extension;
		  Image::make($photo_upload)->resize(1600,800)->save(base_path('public/uploads/banner/'.$photo_name),100);
		  Banner::find($request->banner_id)->update([
		  'header_banner'          => $photo_name,
		]);
		}
		else {
		  //delete
		  $delete_photo=Banner::find($request->banner_id)->header_banner;
		  unlink(base_path('public/uploads/banner/'.$delete_photo));
		  //update
		  $photo_upload     = $request->header_banner;
		  $photo_extension  =  $photo_upload->getClientOriginalExtension();
		  $photo_name       =  $request->banner_id . "." . $photo_extension;
		  Image::make($photo_upload)->resize(1600,800)->save(base_path('public/uploads/banner/'.$photo_name),100);
		  Banner::find($request->banner_id)->update([
		  'header_banner'          => $photo_name,
		]);
		}
	      }
      
//Ajax


	<script type="text/javascript">
	    $(document).ready(function() {
		$('#district').change(function() {
		    var district_id = $(this).val();
		    // alert(district_id);

		    // ajax setup

		    $.ajaxSetup({
			headers: {
			    'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')
			}
		    });

		    // ajax setup request start

		    $.ajax({
			type: 'POST',
			url: '/get/city/list',
			data: {
			    district_id: district_id
			},
			success: function(data) {
			    $("#city").html(data);

			    // alert(data);

			}
		    });

		    // ajax setup request end

		});
	    });
	</script>

      
  //git solution
  
  	$ cd ~/.ssh
	$ ls
   	$ ssh-keygen -o
	//optional
	$ cat ~/.ssh/id_rsa.pub
   
   
   
       
    
 // CDN Link For Sweetalert2 
 https://cdnjs.cloudflare.com/ajax/libs/limonte-sweetalert2/8.11.8/sweetalert2.all.js
 
 
   
 //laravel Validation
public function store(Request $request)
{
    $validatedData = $request->validate([
        'title' => 'required|unique:posts|max:255',
        'body' => 'required',
	
	
	then declare veriables
    ]);

    // The blog post is valid...
}
   
   
