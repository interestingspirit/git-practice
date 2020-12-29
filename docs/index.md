## 多图预览组件

可预览图片，pdf,放大,缩小,旋转

### 方法一

```tsx
import React, { useState, useRef, useEffect } from 'react';
import { Button } from 'antd';
import { Viewer } from 'nuonuo-comp';

const ButtonGroup = Button.Group;

const App = () => {
  const [visible, setVisible] = useState(false);
  const [inline, setInline] = useState(false);
  const containerRef = useRef<HTMLDivElement>(null);

  const images = [
    {
      navSrc: 'https://fengyuanchen.github.io/viewerjs/images/tibet-2.jpg',
      src: 'https://fengyuanchen.github.io/viewerjs/images/tibet-2.jpg',
      fileType: 'jpg',
      alt: '0',
      downloadUrl: '',
    },
    {
      navSrc: 'https://fengyuanchen.github.io/viewerjs/images/tibet-8.jpg',
      src: 'https://fengyuanchen.github.io/viewerjs/images/tibet-8.jpg',
      fileType: 'jpg',
      alt: '1',
      downloadUrl: '',
    },
    {
      navSrc: 'https://fengyuanchen.github.io/viewerjs/images/tibet-9.jpg',
      src: 'https://fengyuanchen.github.io/viewerjs/images/tibet-9.jpg',
      fileType: 'jpg',
      alt: '2',
      downloadUrl: '',
    },
  ];

  type Mode = 'modal' | 'inline';

  const changeMode = (mode: Mode) => {
    if (mode === 'inline') {
      setInline(true);
    } else if (mode === 'modal') {
      setInline(false);
    }
    setVisible(true);
  };

  useEffect(() => {
    changeMode('inline');
  }, []);

  return (
    <>
      <ButtonGroup>
        <Button
          type={inline ? undefined : 'primary'}
          onClick={() => changeMode('modal')}
        >
          Modal Mode
        </Button>
        <Button
          type={inline ? 'primary' : undefined}
          onClick={() => changeMode('inline')}
        >
          Inline Mode
        </Button>
      </ButtonGroup>
      <div ref={containerRef} style={{ height: 500 }}></div>
      <Viewer
        visible={visible}
        onClose={() => setVisible(false)}
        images={images}
        container={
          inline && containerRef.current ? containerRef.current : undefined
        }
      />
    </>
  );
};

export default App;
```

### 方法二

<code src="../src/ImagesViewerReact/index.tsx" />
