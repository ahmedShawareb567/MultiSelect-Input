<template lang="pug">
.filesUploader
  input(type="file" multiple)
  p.mb-0.filesUploader-danger.mt-md(v-if="errors && errors.length") {{errors[0]}}
</template>
<script>
import { compressAccurately } from "image-conversion";

import * as FilePond from "filepond";
import "filepond/dist/filepond.min.css";
import "filepond-plugin-image-preview/dist/filepond-plugin-image-preview.css";

import FilePondPluginFileValidateType from "filepond-plugin-file-validate-type";
import FilePondPluginImagePreview from "filepond-plugin-image-preview";
import FilePondPluginFileValidateSize from "filepond-plugin-file-validate-size";
import FilePondPluginImageCrop from "filepond-plugin-image-crop";
import FilePondPluginImageTransform from "filepond-plugin-image-transform";
import FilePondPluginFileEncode from "filepond-plugin-file-encode";

FilePond.registerPlugin(
  FilePondPluginFileValidateType,
  FilePondPluginFileValidateSize,
  FilePondPluginImageCrop,
  FilePondPluginFileEncode,
  FilePondPluginImagePreview,
  FilePondPluginImageTransform
);

export default {
  name: "ImagesUploader",
  data() {
    return {
      images: [],
    };
  },
  props: {
    vid: {
      type: String,
      default: null,
    },
    value: {
      type: [String, Object, Array],
      default: null,
    },
    rules: {
      type: [String, Object],
      default: "",
    },
    label: {
      type: String,
      required: true,
    },
    edit: {
      type: Boolean,
      default: false,
      required: false,
    },
  },
  watch: {
    value(val) {
      this.images = val;
    },
  },
  components: {},
  mounted() {
    const inputElement = document.querySelector('input[type="file"]');
    const pond = FilePond.create(inputElement, {
      labelIdle: `
        <div class="pt-xl pb-xl">
          <h4 class="mb-0">Upload Images</h4>
        </div>
      `,
      allowFileSizeValidation: true,
      acceptedFileTypes: ["image/*"],
      maxFileSize: "1MB",
      labelMaxFileSize: `أقصى حجم لكل صوره هو 1 ميجابايت`,
      labelMaxFileSizeExceeded: `لقد تجاوزت الحجم المطلوب`,
      onpreparefile: async (file, output) => {
        let currentName = "";
        let res = await compressAccurately(output, {
          size: 500,
          accuracy: 0.9,
          width: 500,
          height: 500,
        });

        if (res) {
          currentName = output.name.split(".")[0];
          let myFile = new File([res], `${currentName}.webp`, {
            type: res.type,
          });
          this.images.push(myFile);
        }
      },
      onremovefile: async (file, output) => {
        const imageName = output.file.name.split(".")[0];
        this.images.forEach((image, i) => {
          if (image.includes(imageName)) {
            this.images.splice(i, 1);
          }
        });
      },
    });
  },
};
</script>
<style lang="scss">
.filesUploader {
  &-danger {
    font-size: 10px !important;
    color: red !important;
  }
}
</style>
