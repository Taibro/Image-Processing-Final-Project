from roboflow import Roboflow
import shutil

rf = Roboflow(api_key="PXwQ4NqbMHWJHN6A0VTl")
project = rf.workspace("vu-quoc-minh-dang").project("flickrlogos32")
version = project.version(1)
dataset = version.download("yolov8")

dataset_folder_name = "FlickrLogos32-1"

source_dir = f"/content/{dataset_folder_name}"
dest_dir = f"{PROJECT_DIR}/{dataset_folder_name}"

if os.path.exists(source_dir):
    if os.path.exists(dest_dir):
        shutil.rmtree(dest_dir)

    shutil.move(source_dir, dest_dir)
    print(f"Đã lưu Dataset vào: {dest_dir}")
else:
    print("Không tìm thấy folder tải về, hãy kiểm tra lại tên folder.")


import yaml

yaml_path = f"{dest_dir}/data.yaml"

with open(yaml_path, 'r') as f:
    data = yaml.safe_load(f)

# Sửa đường dẫn thành tuyệt đối
data['path'] = dest_dir
data['train'] = 'train/images'
data['val'] = 'valid/images'
data['test'] = 'test/images'

with open(yaml_path, 'w') as f:
    yaml.dump(data, f)
