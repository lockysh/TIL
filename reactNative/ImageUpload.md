# Image Upload
사용한 라이브러리 : https://www.npmjs.com/package/@baronha/react-native-multiple-image-picker

사용이유 : 프로젝트 기능 중에 게시글 올리는 기능을 구현하기 위해서는 한번에 한 장 이상의 사진을 업로드 할 수 있도록 해야했다.(많이 쓰이는 image picker 라이브러리는 한 장 이상의 사진을 선택이 불가능함)

```
  const getProfileImage = async () => {
    try {
      const response = await MultipleImagePicker.openPicker({
        selectedAssets: ProfileImg,
        mediaType: 'image',
        singleSelectedMode: true,
        isExportThumbnail: true,
        isCrop: true,
        isCropCircle: true,
      });
      console.log('response: ', response);
      await setProfileImg(response);
    } catch (e) {
      console.log(e.code, e.message);
    }
  };
```
