#Docker begin:
	https://viblo.asia/p/tim-hieu-co-ban-ve-docker-trong-vong-10-phut-jvElaw4dKkw
	
	https://viblo.asia/p/docker-from-the-beginning-part-i-Eb85oa74Z2G
1. Giới thiệu về docker
	Docker là một nền tảng container hóa đóng gói ứng dụng của bạn và tất cả các phụ thuộc của nó với nhau dưới dạng một container docker
	để đảm bảo ứng dụng của bạn hoạt động trơn tru trong mọi môi trường.

2. Khẩu quyết
	`Build, ship and deploy any application, anywhere`
	+ Build: Đóng gói ứng dụng trong một container
	+ Ship: Vận chuyển container
	+ Deploy: Triển khai, chạy container
	+ Bất cứ ứng dụng nào chạy được trên linux
	+ Tất cả mọi nơi: Laptop, máy chủ, máy ảo, cloud instance... 
	+ Đóng gói phầm mềm dễ dàng
	+ Deploy nhanh
	+ Không cần cấu hình và cái đặt môi trường rườm rà.
	
3. Một số khái niệm cơ bản

	+ Image: 
		- Khuôn mẫu, lớp chứa các file cần thiết để tạo nên 1 container
	  	- Chứa những tài nguyên có sẵn
		- Không được tiếp cận vào memory, cpu, storage
	
	+ Container:
		- Tồn tại trên host với 1 ip
		- Được deploy, run and delete thông qua remote client.
		
	+ Doker engine:
		- Tạo và chạy container
		- Chạy lệnh trong chế độ daemon
		- Linux trở thành máy chủ của docker
		- Container đc deploy, chạy và xóa bỏ thông qua remote client
		
	+ Docker daemon
		- Tiến trình chạy ngầm quản lý các container
		
	+ Docker client
		- Kiểm soát hầu hết các workflow của Docker
		- Giao tiếp với các máy chủ docker thông qua daemon
		
	+ Docker hub
		- Chứa các component docker
		- Cho phép lưu, sử dụng, tìm kiếm docker image
		- Vai trò "ship"
	
		
	https://viblo.asia/p/docker-from-the-beginning-part-iii-3P0lP48blox

	https://viblo.asia/p/docker-from-the-beginning-part-iv-RnB5pwkblPG
4. Ứng dụng<br>

	Step 1: Tạo một application : Chúng ta sẽ tạo một app Nodejs Express, hoạt động như REST API.
	
	Step 2: Tạo Dockerfile: Một file text nói cho Docker build application của chúng ta như thế nào.
	
	Step 3: Build an image: Bước đầu tiên để ứng dụng của chung ta chay được là phải tạo một cái gọi là Docker image.
	
		Tạo docker image từ docker file<br>
		
		`docker build -t chrisnoring/node:latest .`
		
		Hiển thị toàn bộ danh sách image<br>
		`docker images`
		
		Dấu ' .' ở cuối câu lệnh nói cho docker biết là file Dockerfile của bạn nằm ở đâu. Trong trường hợp này thì file Dockerfile nằm ở thư một mà chúng ta đang đứng
		
		Xóa một image<br>
			`docker image rm [môt phần của image_id](hoặc [image_name]:[iamge_tag])`
		
	Step 4: Create a container từ docker image.<br>
			`docker thamso IMAGE command thamsolenh`
			
			`docker run -p [port của máy thực]:[port bên trong docker] [docker_image]`
		
	Sample: <br>
		`docker run -i(muốn nhận tương tác)  -t(kết nối tới terminal: -i -t = -it) --name [Đặt tên cho container] -h [hostname] [name]:[tag](hoặc sử dụng image id)`
	
	nếu đang trong một container để thoát dừng<br>
		`exit`
	
	Để container vẫn chạy bình thường<br>
		`Ctrl + P + Q`
	
	Để restart lại container:<br>
		`docker start [container_id](hoặc names)`
	
	Để vào lại container<br>
		`docker attach [container_id]` hoặc `docker exec -it [container_id] bash`
	
	Để xóa một container<br>
		`docker rm [container_id]`
		
	Để xóa một container đang chạy<br>
		`docker rm [container_id]`
	
	Nếu container vẫn đang chạy, muốn xóa nó.<br>
		`docker rm [container_id] -f`
		
	Nếu bạn muốn thực hiện lệnh trong container_id nhưng đang ở chế độ bên ngoài.<br>
		`docker exec [container_name] [command trong container]`
		
	List all container<br>
		`docker ps -aq`
		
	Stop all running container<br>
		`docker stop $(docker ps -aq)`
		
	Remove all container<br>
		`docker rm $(docker ps -aq) -f`
		
	Remove all image<br>
		`docker rmi $(docker image -q)  -f`
		
	Để cài đặt htop trong ubuntu<br>
		`apt update`
		`apt install htop`
		
	Để lưu lại 1 container thành 1 image.<br>
		Step 1: docker images
		Step 2: dừng docker container lại
		Step 3: `docker commit [container_id] [image_name]`
		Step 4: Lưu thành 1 docker file
			`docker save --output [file_name].tar [image_id]`
		
	Để load 1 docker image từ docker file<br>
		Step 1: `docker load -i [docker_file_name]`
		Step 2: Đặt tên cho image
			`docker tag f [image_name]:[image_tag]`
	** Lưu ý: Nếu không start được thì restart docker.

	docker manager:<br>
		`docker ps // show tất cả các container đang chạy.
		`docker stop [container id] // stop contaner theo container theo id được chỉ định.
		`docker exec -it [container id] bash // khi chạy lệnh này thì command line bạn chạy tiếp theo sẽ được thực hiện bên trong OS của docker.

5. Chia sẻ dữ liệu trong Docker, tạo và quản lý ổ đĩa docker volume
	https://viblo.asia/p/docker-from-the-beginning-part-ii-GrLZD8X3Zk0
	Để chia sẻ ổ đĩa từ ngoài vào trong ổ trên container của docker<br>
		`docker run -it -v(để chia sẻ máy host vs container) [thư mục trên máy host]:[ánh xạ tới thư mục container]`
		
		
	Để chia sẻ dữ liệu giữa các container với nhau<br>
		`docker run -it --name [container_name] --volumes-from [container_name_from](hoặc là container_id_from) [image_id]`
	
	Docker Volume<br>
		- Create docker container thông qua docker image: docker run -d -p 8000:3000 chrisnoring/node        <chạy một container ở port 8000(-p) và ở chế độ detached(-d)>
		
		- Theo cách thông thường, nếu không có docker volume thì sẽ phải thực hiện lại các step như sau:
		
			`docker stop my-container` // this will stop the container, it can still be started if we want to

			`docker rm my-container` // this will remove the container completely

			`docker build -t chrisnoring/node .` // creates an image

			`docker run -d -p 8000:3000 --name [containerId] [image_name]`
	
		Step 1: Create docker volume<br>
			`docker volume create [name of volume]`
			
			Liệt kê danh sách docker volume
				`docker volume ls`
				
			Để remove volume
				`docker volume prune` // remove tất cả các volume đã được tạo.
				`docker volume rm [name of volume]` //remove volume có tên là [name of volume]
				
			Để xem thông tin chi tiết của docker volume
				`docker inspect [name of volume]`
		Step 2: Gắn kết một volume trong application<br>
			-v, —-volume, cú pháp như sau -v [name of volume]:[directory in the container], ví dụ -v my-volume:/app
			--mount, cú pháp như sau --mount source=[name of volume],target=[directory in container] , ví dụ —-mount source=my-volume,target=/app Khi được sử dụng kết hợp với việc chạy một container, nó sẽ trông như thế sau:
			
			`docker run -it --name [container_name] --mount(gán ổ đĩa) source=[volume_name],target=[path_folder_in_container] [image_id]`
		
			Kiểm tra xem volume có còn dữ liệu k?
			
			
		Step 3: Thao tác với app của chúng ta như một volume<br>
		
	Tạo một ổ đĩa ánh xạ tới một thư mục cụ thể nào đó mà chúng ta ấn định ra ở trong máy host.	<br>
	
		`docker volume create --opt(Định nghĩa giá trị options) device=[path_folder_host] --opt type=none --opt o=bind [volume_name]`
		
	Tạo container ánh xạ tơi ổ đĩa vừa tạo<br>
		`docker run -it -v [DISK_NAME]:[path_container] [imageId]`
		
		
	Để xóa toàn bộ docker volume <br>
		`docker volume rm $(docker volume ls -q)`
6. Mạng trong docker, quản lý network trong docker<br>

	Install busybox<br>
		`docker pull busybox`
		
	Create 1 container từ image busybox<br>
		`docker run -it --rm(Xóa container khi container kết thúc) busybox`
		
	List các lệnh trong busybox<br>
		`ls /bin/ -la`
		
	Kiểm tra xem trong docker có những mạng nào<br>
		`docker network ls`
		
	Ánh xạ cổng x -> y: Khi thực hiện ánh xạ xong thì chúng ta có thể truy cập từ trình duyệt bên ngoài vào trong mạng container của docker<br>
		`docker run -it --name [container_name] -p(Ánh xạ cổng) [cổng ánh xạ]:[cổng mặc định của container] [image_name]`
		
	Tạo ra các bản cầu mạng khác nhau, nếu không chỉ định loại network thì sẽ mặc định là bridge<br>
		`docker network create --driver [loại network] [network_name]`
		
	Create container sử dụng network do mình tạo ra<br>
		`docker run -it --name [container_name] --network [network_name] [image_name]`
	Để cho một container connect tới một network<br>
		`docker network connect [network_name] [container_name]`
		
7. Chạy Apache Httpd
	
	
8. Chạy Mysql
		`docker pull mysql`
		
		`docker run -it -rm -e param1=value1 param2=value 2 [image_name]`
