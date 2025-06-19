# Card Showcase With Hover Effect

1. Component `CardShowcase.jsx`

```
import { useRef } from "react";
import "./CardShowcase.css"; // CSS file for styles

const cardData = {
    link: "https://github.com/Id-Yuu",
    image: "https://images.unsplash.com/photo-1627467658687-4accff8724a5",
    logo: "https://react.dev/_next/image?url=%2Fimages%2Fuwu.png&w=384&q=75",
    title: "Card Image Hover Effect",
    subtitle: "Created with React and CSS",
};

export default function CardShowcase() {
    const cardRef = useRef(null);
    const logoRef = useRef(null);
    const logoInnerRef = useRef(null);
    const imgRef = useRef(null);

    // Mouse move effect
    const handleMouseMove = (e) => {
        const card = cardRef.current;
        const logo = logoRef.current;
        const logoInner = logoInnerRef.current;
        const charImg = imgRef.current;

        if (!card) return;

        const { left, top, width, height } = card.getBoundingClientRect();
        const centerX = left + width / 2;
        const centerY = top + height / 2;

        const getOffset = (cursor, center, limit = 20) => {
            const delta = cursor - center;
            return Math.max(Math.min(delta, limit), -limit);
        };

        const getBrightness = (cursorY, centerY, strength = 20) => {
            return 1 - (getOffset(cursorY, centerY) / strength) * 0.05;
        };

        const offsetX = getOffset(e.clientX, centerX);
        const offsetY = getOffset(e.clientY, centerY);
        const rawX = e.clientX - centerX;
        const rawY = e.clientY - centerY;

        card.style.transform = `translateZ(0) perspective(1000px) rotateY(${offsetX}deg) rotateX(${-offsetY / 1.5}deg)`;
        card.style.filter = `brightness(${getBrightness(e.clientY, centerY)})`;
        card.style.boxShadow = `${-offsetX}px ${-offsetY}px 10px rgba(0, 0, 20, 0.25)`;

        if (logoInner) {
            logoInner.style.left = `${rawX / 10}px`;
            logoInner.style.top = `${rawY / 15}px`;
        }

        if (logo) {
            logo.style.filter = `drop-shadow(${-offsetX / 7}px ${-offsetY / 7}px 0px white)`;
        }

        if (charImg) {
            charImg.style.left = `${rawX / 8}px`;
            charImg.style.top = `${rawY / 13}px`;
            charImg.style.filter = `drop-shadow(${-offsetX / 2}px ${-offsetY / 2}px 5px rgba(0,0,20,0.2))`;
        }
    };

    // Mouse leave effect
    const handleMouseLeave = () => {
        const card = cardRef.current;
        const logo = logoRef.current;
        const logoInner = logoInnerRef.current;
        const charImg = imgRef.current;

        card.style.transform = "perspective(500px) scale(1)";
        card.style.filter = "brightness(1) drop-shadow(0px 5px 5px rgba(0,0,0,.5))";
        card.style.boxShadow = "0 0 0 0 rgba(0,0,0,0.2)";
        if (charImg) {
            charImg.style.left = "0";
            charImg.style.top = "0";
            charImg.style.filter = "none";
        }
        if (logo) {
            logo.style.left = "0";
            logo.style.top = "0";
            logo.style.filter = "none";
            logo.style.transform = "translateZ(0) scale(1)";
            logo.style.overflow = "hidden";
        }
        if (logoInner) {
            logoInner.style.left = "0";
            logoInner.style.top = "0";
        }
    };

    // Mouse enter effect
    const handleMouseEnter = () => {
        const logo = logoRef.current;
        const card = cardRef.current;
        card.style.zIndex = "1";
        if (logo) {
            logo.style.overflow = "inherit";
            logo.style.left = "-20px";
            logo.style.top = "-30px";
            logo.style.transform = "scale(0.7)";
        }
        setTimeout(() => {
            card.style.transition = "all 0s ease";
        }, 300);
    };

    return (
        <div className="cardShowcasePage">
            <div className="cardShowcaseHalfList">
                <div className="cardShowcaseContainer">
                    <div
                        className="cardShowcaseOuter"
                        ref={cardRef}
                        onMouseMove={handleMouseMove}
                        onMouseLeave={handleMouseLeave}
                        onMouseEnter={handleMouseEnter}
                    >
                        <a href={cardData.link}>
                            <div className="cardShowcaseBg"></div>
                            <div className="cardShowcaseImgArea">
                                <div className="cardShowcaseDots"></div>
                            </div>
                            <div className="cardShowcaseImgArea inherit">
                                <div className="cardShowcaseImg" ref={imgRef}>
                                    <img src={cardData.image} width="120" alt={cardData.title} />
                                </div>
                            </div>
                            <div className="cardShowcaseLogoArea" ref={logoRef}>
                                <div className="cardShowcaseLogo" ref={logoInnerRef}>
                                    <div className="cardShowcaseLogoBrand">
                                        <img src={cardData.logo} width="100%" alt="brand" />
                                    </div>
                                </div>
                            </div>
                            <div className="cardShowcaseTitle">{cardData.title}</div>
                            <div className="cardShowcaseSubtitle">{cardData.subtitle}</div>
                        </a>
                    </div>
                </div>
            </div>
        </div>
    );
}
```

2. style `CardShowcase.css`

```
.cardShowcaseOuter {
  width: 120px;
  height: 276px;
  background: #fff;
  position: relative;
  margin: 0;
  font-size: 0;
  display: inline-block;
  filter: drop-shadow(0px 5px 5px rgba(0, 0, 0, 0.5));
  cursor: pointer;
  transition: all 0.4s ease;
}

.cardShowcaseBg {
  position: absolute;
  top: 0;
  left: 0;
  background: #fff;
  width: 120px;
  height: 240px;
  z-index: 0;
}

.cardShowcaseImgArea {
  position: absolute;
  bottom: 36px;
  left: 0;
  width: 120px;
  z-index: 1;
  overflow: hidden;
}

.cardShowcaseImgArea.inherit {
  overflow: inherit;
}

.cardShowcaseDots {
  position: absolute;
  right: -50px;
  bottom: -33px;
  width: 200px;
  height: 100px;
  background: radial-gradient(rgba(0, 0, 0, 0.2) 6%, transparent 7%);
  z-index: 0;
}

.cardShowcaseImg {
  position: relative;
  z-index: 1;
}

.cardShowcaseLogoArea {
  position: absolute;
  top: 0;
  width: 120px;
  height: 240px;
  overflow: hidden;
  z-index: 0;
  transition: all 0.4s ease;
  transform-origin: left top;
}

.cardShowcaseLogo {
  filter: invert();
  opacity: 0.81;
  position: relative;
}

.cardShowcaseLogoBrand {
  position: absolute;
  top: 50px;
  left: -10px;
  width: 120px;
}

.cardShowcaseTitle {
  position: absolute;
  top: 244px;
  left: 4px;
  color: #5b5b5b;
  font-weight: bold;
  font-size: 13px;
  line-height: 12px;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  max-width: 95%;
}

.cardShowcaseSubtitle {
  position: absolute;
  bottom: 4px;
  left: 4px;
  color: #5b5b5b;
  font-size: 10px;
  line-height: 12px;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  max-width: 95%;
}
```

3. call component
```
import CardShowcase from './components/CardShowcase';

<CardShowcase />
```
