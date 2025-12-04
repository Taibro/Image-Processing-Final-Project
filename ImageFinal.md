import gradio as gr

def predict_logo(image_path):
    results = model.predict(source=image_path, save=True, exist_ok=True)

    result_path = results[0].save_dir
    output_image_path = os.path.join(result_path, os.path.basename(image_path))

    return output_image_path


iface = gr.Interface(
    fn=predict_logo,
    inputs=gr.Image(type="filepath", label="Tải lên ảnh cần nhận diện Logo"),
    outputs=gr.Image(label="Kết quả Phát hiện Logo"),
    title="Demo Phát hiện và Phân loại Logo bằng YOLOv8"
)

iface.launch(share=True)
